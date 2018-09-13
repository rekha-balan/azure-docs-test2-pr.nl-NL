#### <a name="configure-the-ios-project-in-xamarin-studio"></a><span data-ttu-id="17cb9-101">Configure the iOS project in Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="17cb9-101">Configure the iOS project in Xamarin Studio</span></span>
1. <span data-ttu-id="17cb9-102">In Xamarin.Studio, open **Info.plist**, and update the **Bundle Identifier** with the bundle ID that you created earlier with your new app ID.</span><span class="sxs-lookup"><span data-stu-id="17cb9-102">In Xamarin.Studio, open **Info.plist**, and update the **Bundle Identifier** with the bundle ID that you created earlier with your new app ID.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. <span data-ttu-id="17cb9-103">Scroll down to **Background Modes**.</span><span class="sxs-lookup"><span data-stu-id="17cb9-103">Scroll down to **Background Modes**.</span></span> <span data-ttu-id="17cb9-104">Select the **Enable Background Modes** box and the **Remote notifications** box.</span><span class="sxs-lookup"><span data-stu-id="17cb9-104">Select the **Enable Background Modes** box and the **Remote notifications** box.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. <span data-ttu-id="17cb9-105">Double-click your project in the Solution Panel to open **Project Options**.</span><span class="sxs-lookup"><span data-stu-id="17cb9-105">Double-click your project in the Solution Panel to open **Project Options**.</span></span>
4. <span data-ttu-id="17cb9-106">Under **Build**, choose **iOS Bundle Signing**, and select the corresponding identity and provisioning profile you just set up for this project.</span><span class="sxs-lookup"><span data-stu-id="17cb9-106">Under **Build**, choose **iOS Bundle Signing**, and select the corresponding identity and provisioning profile you just set up for this project.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   <span data-ttu-id="17cb9-107">This ensures that the project uses the new profile for code signing.</span><span class="sxs-lookup"><span data-stu-id="17cb9-107">This ensures that the project uses the new profile for code signing.</span></span> <span data-ttu-id="17cb9-108">For the official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span><span class="sxs-lookup"><span data-stu-id="17cb9-108">For the official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>

#### <a name="configure-the-ios-project-in-visual-studio"></a><span data-ttu-id="17cb9-109">Configure the iOS project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="17cb9-109">Configure the iOS project in Visual Studio</span></span>
1. <span data-ttu-id="17cb9-110">In Visual Studio, right-click the project, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="17cb9-110">In Visual Studio, right-click the project, and then click **Properties**.</span></span>
2. <span data-ttu-id="17cb9-111">In the properties pages, click the **iOS Application** tab, and update the **Identifier** with the ID that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="17cb9-111">In the properties pages, click the **iOS Application** tab, and update the **Identifier** with the ID that you created earlier.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. <span data-ttu-id="17cb9-112">In the **iOS Bundle Signing** tab, select the corresponding identity and provisioning profile you just set up for this project.</span><span class="sxs-lookup"><span data-stu-id="17cb9-112">In the **iOS Bundle Signing** tab, select the corresponding identity and provisioning profile you just set up for this project.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    <span data-ttu-id="17cb9-113">This ensures that the project uses the new profile for code signing.</span><span class="sxs-lookup"><span data-stu-id="17cb9-113">This ensures that the project uses the new profile for code signing.</span></span> <span data-ttu-id="17cb9-114">For the official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span><span class="sxs-lookup"><span data-stu-id="17cb9-114">For the official Xamarin device provisioning documentation, see [Xamarin Device Provisioning].</span></span>
4. <span data-ttu-id="17cb9-115">Double-click Info.plist to open it, and then enable **RemoteNotifications** under **Background Modes**.</span><span class="sxs-lookup"><span data-stu-id="17cb9-115">Double-click Info.plist to open it, and then enable **RemoteNotifications** under **Background Modes**.</span></span>

[Xamarin Device Provisioning]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/





