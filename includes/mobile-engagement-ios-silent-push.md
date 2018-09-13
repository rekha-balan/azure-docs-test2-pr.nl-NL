> [!IMPORTANT]
> <span data-ttu-id="5841c-101">To receive Push Notifications from Mobile Engagement, you need to enable `Silent Remote Notifications` in your application.</span><span class="sxs-lookup"><span data-stu-id="5841c-101">To receive Push Notifications from Mobile Engagement, you need to enable `Silent Remote Notifications` in your application.</span></span> <span data-ttu-id="5841c-102">You need to add the remote-notification value to the UIBackgroundModes array in your Info.plist file.</span><span class="sxs-lookup"><span data-stu-id="5841c-102">You need to add the remote-notification value to the UIBackgroundModes array in your Info.plist file.</span></span>
> 
> 

1. <span data-ttu-id="5841c-103">Open `info.plist` file in the project</span><span class="sxs-lookup"><span data-stu-id="5841c-103">Open `info.plist` file in the project</span></span>
2. <span data-ttu-id="5841c-104">Right click on the top item in the list (`Information Property List`) and add a new row</span><span class="sxs-lookup"><span data-stu-id="5841c-104">Right click on the top item in the list (`Information Property List`) and add a new row</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. <span data-ttu-id="5841c-105">In the new row enter `Required background modes`</span><span class="sxs-lookup"><span data-stu-id="5841c-105">In the new row enter `Required background modes`</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. <span data-ttu-id="5841c-106">Click on the left arrow to expand the row</span><span class="sxs-lookup"><span data-stu-id="5841c-106">Click on the left arrow to expand the row</span></span>
5. <span data-ttu-id="5841c-107">Add the following value to the item 0 `App downloads content in response to push notifications`</span><span class="sxs-lookup"><span data-stu-id="5841c-107">Add the following value to the item 0 `App downloads content in response to push notifications`</span></span>
   
    ![](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. <span data-ttu-id="5841c-108">Once you make the change, the info.plist XML should contain the following key and value:</span><span class="sxs-lookup"><span data-stu-id="5841c-108">Once you make the change, the info.plist XML should contain the following key and value:</span></span>
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. <span data-ttu-id="5841c-109">If you are using **Xcode 7+** and **iOS 9+**:</span><span class="sxs-lookup"><span data-stu-id="5841c-109">If you are using **Xcode 7+** and **iOS 9+**:</span></span>
   
   * <span data-ttu-id="5841c-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span><span class="sxs-lookup"><span data-stu-id="5841c-110">Enable **Push Notifications** in Targets > Your Target Name > Capabilities.</span></span>




