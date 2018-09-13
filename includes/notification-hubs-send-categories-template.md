
<span data-ttu-id="5577d-101">This section shows how to send breaking news as tagged template notifications from a .NET console app.</span><span class="sxs-lookup"><span data-stu-id="5577d-101">This section shows how to send breaking news as tagged template notifications from a .NET console app.</span></span>

<span data-ttu-id="5577d-102">If you are using Mobile Apps please refer to the [Add push notifications for Mobile Apps] tutorial and select your platform at the top.</span><span class="sxs-lookup"><span data-stu-id="5577d-102">If you are using Mobile Apps please refer to the [Add push notifications for Mobile Apps] tutorial and select your platform at the top.</span></span>

<span data-ttu-id="5577d-103">If you want to use Java or PHP refer to [How to use Notification Hubs from Java/PHP].</span><span class="sxs-lookup"><span data-stu-id="5577d-103">If you want to use Java or PHP refer to [How to use Notification Hubs from Java/PHP].</span></span> <span data-ttu-id="5577d-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span><span class="sxs-lookup"><span data-stu-id="5577d-104">You can send notifications from any backend using the [Notification Hubs REST interface].</span></span>

<span data-ttu-id="5577d-105">Skip steps 1-3 if you created the console app for sending notifications when you completed [Get started with Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="5577d-105">Skip steps 1-3 if you created the console app for sending notifications when you completed [Get started with Notification Hubs].</span></span>

1. <span data-ttu-id="5577d-106">In Visual Studio create a new Visual C# console application:</span><span class="sxs-lookup"><span data-stu-id="5577d-106">In Visual Studio create a new Visual C# console application:</span></span>
   
       ![][13]
2. <span data-ttu-id="5577d-107">In the Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in the console window type the  following and press **Enter**:</span><span class="sxs-lookup"><span data-stu-id="5577d-107">In the Visual Studio main menu, click **Tools**, **Library Package Manager**, and **Package Manager Console**, then in the console window type the  following and press **Enter**:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="5577d-108">This adds a reference to the Azure Notification Hubs SDK using the [Microsoft.Azure.Notification Hubs NuGet package].</span><span class="sxs-lookup"><span data-stu-id="5577d-108">This adds a reference to the Azure Notification Hubs SDK using the [Microsoft.Azure.Notification Hubs NuGet package].</span></span>
3. <span data-ttu-id="5577d-109">Open the file Program.cs and add the following `using` statement:</span><span class="sxs-lookup"><span data-stu-id="5577d-109">Open the file Program.cs and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="5577d-110">In the `Program` class, add the following method, or replace it if it already exists:</span><span class="sxs-lookup"><span data-stu-id="5577d-110">In the `Program` class, add the following method, or replace it if it already exists:</span></span>
   
        private static async void SendTemplateNotificationAsync()
        {
            // Define the notification hub.
            NotificationHubClient hub =
                NotificationHubClient.CreateClientFromConnectionString(
                    "<connection string with full access>", "<hub name>");
   
            // Create an array of breaking news categories.
            var categories = new string[] { "World", "Politics", "Business",
                                            "Technology", "Science", "Sports"};
   
            // Sending the notification as a template notification. All template registrations that contain
            // "messageParam" and the proper tags will receive the notifications.
            // This includes APNS, GCM, WNS, and MPNS template registrations.
   
            Dictionary<string, string> templateParams = new Dictionary<string, string>();
   
            foreach (var category in categories)
            {
                templateParams["messageParam"] = "Breaking " + category + " News!";
                await hub.SendTemplateNotificationAsync(templateParams, category);
            }
         }
   
    <span data-ttu-id="5577d-111">This code sends a template notification for each of the six tags in the string array.</span><span class="sxs-lookup"><span data-stu-id="5577d-111">This code sends a template notification for each of the six tags in the string array.</span></span> <span data-ttu-id="5577d-112">The use of tags makes sure that devices receive notifications only for the registered categories.</span><span class="sxs-lookup"><span data-stu-id="5577d-112">The use of tags makes sure that devices receive notifications only for the registered categories.</span></span>
5. <span data-ttu-id="5577d-113">In the above code, replace the `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and the connection  string for *DefaultFullSharedAccessSignature* from the dashboard of your notification hub.</span><span class="sxs-lookup"><span data-stu-id="5577d-113">In the above code, replace the `<hub name>` and `<connection string with full access>` placeholders with your notification hub name and the connection  string for *DefaultFullSharedAccessSignature* from the dashboard of your notification hub.</span></span>
6. <span data-ttu-id="5577d-114">Add the following lines in the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="5577d-114">Add the following lines in the **Main** method:</span></span>
   
         SendTemplateNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="5577d-115">Build the console app.</span><span class="sxs-lookup"><span data-stu-id="5577d-115">Build the console app.</span></span>

<!-- Images. -->
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-back-end/notification-hub-create-console-app.png

<!-- URLs. -->
[Get started with Notification Hubs]: ../articles/notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Notification Hubs REST interface]: http://msdn.microsoft.com/library/windowsazure/dn223264.aspx
[Add push notifications for Mobile Apps]: ../articles/app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md
[How to use Notification Hubs from Java/PHP]: ../articles/notification-hubs/notification-hubs-java-push-notification-tutorial.md
[Microsoft.Azure.Notification Hubs NuGet package]: http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/

