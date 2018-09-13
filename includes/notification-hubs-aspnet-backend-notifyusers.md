## <a name="create-the-webapi-project"></a><span data-ttu-id="cc728-101">Create the WebAPI Project</span><span class="sxs-lookup"><span data-stu-id="cc728-101">Create the WebAPI Project</span></span>
<span data-ttu-id="cc728-102">A new ASP.NET WebAPI backend will be created in the sections that follow and it will have three main purposes:</span><span class="sxs-lookup"><span data-stu-id="cc728-102">A new ASP.NET WebAPI backend will be created in the sections that follow and it will have three main purposes:</span></span>

1. <span data-ttu-id="cc728-103">**Authenticating Clients**: A message handler will be added later to authenticate client requests and associate the user with the request.</span><span class="sxs-lookup"><span data-stu-id="cc728-103">**Authenticating Clients**: A message handler will be added later to authenticate client requests and associate the user with the request.</span></span>
2. <span data-ttu-id="cc728-104">**Client Notification Registrations**: Later, you will add a controller to handle new registrations for a client device to receive notifications.</span><span class="sxs-lookup"><span data-stu-id="cc728-104">**Client Notification Registrations**: Later, you will add a controller to handle new registrations for a client device to receive notifications.</span></span> <span data-ttu-id="cc728-105">The authenticated user name will automatically be added to the registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc728-105">The authenticated user name will automatically be added to the registration as a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx).</span></span>
3. <span data-ttu-id="cc728-106">**Sending Notifications to Clients**: Later, you will also add a controller to provide a way for a user to trigger a secure push to devices and clients associated with the tag.</span><span class="sxs-lookup"><span data-stu-id="cc728-106">**Sending Notifications to Clients**: Later, you will also add a controller to provide a way for a user to trigger a secure push to devices and clients associated with the tag.</span></span> 

<span data-ttu-id="cc728-107">The following steps show how to create the new ASP.NET WebAPI backend:</span><span class="sxs-lookup"><span data-stu-id="cc728-107">The following steps show how to create the new ASP.NET WebAPI backend:</span></span> 

> [!NOTE]
> <span data-ttu-id="cc728-108">**Important**: Before starting this tutorial, please ensure that you have installed the latest version of the NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="cc728-108">**Important**: Before starting this tutorial, please ensure that you have installed the latest version of the NuGet Package Manager.</span></span> <span data-ttu-id="cc728-109">To check, start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cc728-109">To check, start Visual Studio.</span></span> <span data-ttu-id="cc728-110">From the **Tools** menu, click **Extensions and Updates**.</span><span class="sxs-lookup"><span data-stu-id="cc728-110">From the **Tools** menu, click **Extensions and Updates**.</span></span> <span data-ttu-id="cc728-111">Search for **NuGet Package Manager for Visual Studio 2013**, and make sure you have version 2.8.50313.46 or later.</span><span class="sxs-lookup"><span data-stu-id="cc728-111">Search for **NuGet Package Manager for Visual Studio 2013**, and make sure you have version 2.8.50313.46 or later.</span></span> <span data-ttu-id="cc728-112">If not, please uninstall, then reinstall the NuGet Package Manager.</span><span class="sxs-lookup"><span data-stu-id="cc728-112">If not, please uninstall, then reinstall the NuGet Package Manager.</span></span>
> 
> ![][B4]
> 
> [!NOTE]
> <span data-ttu-id="cc728-113">Make sure you have installed the Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span><span class="sxs-lookup"><span data-stu-id="cc728-113">Make sure you have installed the Visual Studio [Azure SDK](https://azure.microsoft.com/downloads/) for website deployment.</span></span>
> 
> 

1. <span data-ttu-id="cc728-114">Start Visual Studio or Visual Studio Express.</span><span class="sxs-lookup"><span data-stu-id="cc728-114">Start Visual Studio or Visual Studio Express.</span></span> <span data-ttu-id="cc728-115">Click **Server Explorer** and sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="cc728-115">Click **Server Explorer** and sign in to your Azure account.</span></span> <span data-ttu-id="cc728-116">Visual Studio will need you signed in to create the web site resources on your account.</span><span class="sxs-lookup"><span data-stu-id="cc728-116">Visual Studio will need you signed in to create the web site resources on your account.</span></span>
2. <span data-ttu-id="cc728-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type the name **AppBackend**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc728-117">In Visual Studio, click **File**, then click **New**, then **Project**, expand **Templates**, **Visual C#**, then click **Web** and **ASP.NET Web Application**, type the name **AppBackend**, and then click **OK**.</span></span> 
   
    ![][B1]
3. <span data-ttu-id="cc728-118">In the **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="cc728-118">In the **New ASP.NET Project** dialog, click **Web API**, then click **OK**.</span></span>
   
    ![][B2]
4. <span data-ttu-id="cc728-119">In the **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span><span class="sxs-lookup"><span data-stu-id="cc728-119">In the **Configure Microsoft Azure Web App** dialog, choose a subscription, and an **App Service plan** you have already created.</span></span> <span data-ttu-id="cc728-120">You can also choose **Create a new app service plan** and create one from the dialog.</span><span class="sxs-lookup"><span data-stu-id="cc728-120">You can also choose **Create a new app service plan** and create one from the dialog.</span></span> <span data-ttu-id="cc728-121">You do not need a database for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="cc728-121">You do not need a database for this tutorial.</span></span> <span data-ttu-id="cc728-122">Once you have selected your app service plan, click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="cc728-122">Once you have selected your app service plan, click **OK** to create the project.</span></span>
   
    ![][B5]

## <a name="authenticating-clients-to-the-webapi-backend"></a><span data-ttu-id="cc728-123">Authenticating Clients to the WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="cc728-123">Authenticating Clients to the WebAPI Backend</span></span>
<span data-ttu-id="cc728-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for the new backend.</span><span class="sxs-lookup"><span data-stu-id="cc728-124">In this section, you will create a new message handler class named **AuthenticationTestHandler** for the new backend.</span></span> <span data-ttu-id="cc728-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into the backend.</span><span class="sxs-lookup"><span data-stu-id="cc728-125">This class is derived from [DelegatingHandler](https://msdn.microsoft.com/library/system.net.http.delegatinghandler.aspx) and added as a message handler so it can process all requests coming into the backend.</span></span> 

1. <span data-ttu-id="cc728-126">In Solution Explorer, right-click the **AppBackend** project, click **Add**, then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="cc728-126">In Solution Explorer, right-click the **AppBackend** project, click **Add**, then click **Class**.</span></span> <span data-ttu-id="cc728-127">Name the new class **AuthenticationTestHandler.cs**, and click **Add** to generate the class.</span><span class="sxs-lookup"><span data-stu-id="cc728-127">Name the new class **AuthenticationTestHandler.cs**, and click **Add** to generate the class.</span></span> <span data-ttu-id="cc728-128">This class will be used to authenticate users using *Basic Authentication* for simplicity.</span><span class="sxs-lookup"><span data-stu-id="cc728-128">This class will be used to authenticate users using *Basic Authentication* for simplicity.</span></span> <span data-ttu-id="cc728-129">Note that your app can use any authentication scheme.</span><span class="sxs-lookup"><span data-stu-id="cc728-129">Note that your app can use any authentication scheme.</span></span>
2. <span data-ttu-id="cc728-130">In AuthenticationTestHandler.cs, add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="cc728-130">In AuthenticationTestHandler.cs, add the following `using` statements:</span></span>
   
        using System.Net.Http;
        using System.Threading;
        using System.Security.Principal;
        using System.Net;
        using System.Web;
3. <span data-ttu-id="cc728-131">In AuthenticationTestHandler.cs, replacing the `AuthenticationTestHandler` class definition with the following code.</span><span class="sxs-lookup"><span data-stu-id="cc728-131">In AuthenticationTestHandler.cs, replacing the `AuthenticationTestHandler` class definition with the following code.</span></span> 
   
    <span data-ttu-id="cc728-132">This handler will authorize the request when the following three conditions are all true:</span><span class="sxs-lookup"><span data-stu-id="cc728-132">This handler will authorize the request when the following three conditions are all true:</span></span>
   
   * <span data-ttu-id="cc728-133">The request included an *Authorization* header.</span><span class="sxs-lookup"><span data-stu-id="cc728-133">The request included an *Authorization* header.</span></span> 
   * <span data-ttu-id="cc728-134">The request uses *basic* authentication.</span><span class="sxs-lookup"><span data-stu-id="cc728-134">The request uses *basic* authentication.</span></span> 
   * <span data-ttu-id="cc728-135">The user name string and the password string are the same string.</span><span class="sxs-lookup"><span data-stu-id="cc728-135">The user name string and the password string are the same string.</span></span>
     
     <span data-ttu-id="cc728-136">Otherwise, the request will be rejected.</span><span class="sxs-lookup"><span data-stu-id="cc728-136">Otherwise, the request will be rejected.</span></span> <span data-ttu-id="cc728-137">This is not a true authentication and authorization approach.</span><span class="sxs-lookup"><span data-stu-id="cc728-137">This is not a true authentication and authorization approach.</span></span> <span data-ttu-id="cc728-138">It is just a very simple example for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="cc728-138">It is just a very simple example for this tutorial.</span></span>
     
     <span data-ttu-id="cc728-139">If the request message is authenticated and authorized by the `AuthenticationTestHandler`, then the basic authentication user will be attached to the current request on the [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc728-139">If the request message is authenticated and authorized by the `AuthenticationTestHandler`, then the basic authentication user will be attached to the current request on the [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.current.aspx).</span></span> <span data-ttu-id="cc728-140">User information in the HttpContext will be used by another controller (RegisterController) later to add a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) to the notification registration request.</span><span class="sxs-lookup"><span data-stu-id="cc728-140">User information in the HttpContext will be used by another controller (RegisterController) later to add a [tag](https://msdn.microsoft.com/library/azure/dn530749.aspx) to the notification registration request.</span></span>
     
       <span data-ttu-id="cc728-141">public class AuthenticationTestHandler : DelegatingHandler   {</span><span class="sxs-lookup"><span data-stu-id="cc728-141">public class AuthenticationTestHandler : DelegatingHandler   {</span></span>
     
           protected override Task<HttpResponseMessage> SendAsync(
           HttpRequestMessage request, CancellationToken cancellationToken)
           {
               var authorizationHeader = request.Headers.GetValues("Authorization").First();
     
               if (authorizationHeader != null && authorizationHeader
                   .StartsWith("Basic ", StringComparison.InvariantCultureIgnoreCase))
               {
                   string authorizationUserAndPwdBase64 =
                       authorizationHeader.Substring("Basic ".Length);
                   string authorizationUserAndPwd = Encoding.Default
                       .GetString(Convert.FromBase64String(authorizationUserAndPwdBase64));
                   string user = authorizationUserAndPwd.Split(':')[0];
                   string password = authorizationUserAndPwd.Split(':')[1];
     
                   if (verifyUserAndPwd(user, password))
                   {
                       // Attach the new principal object to the current HttpContext object
                       HttpContext.Current.User =
                           new GenericPrincipal(new GenericIdentity(user), new string[0]);
                       System.Threading.Thread.CurrentPrincipal =
                           System.Web.HttpContext.Current.User;
                   }
                   else return Unauthorized();
               }
               else return Unauthorized();
     
               return base.SendAsync(request, cancellationToken);
           }
     
           private bool verifyUserAndPwd(string user, string password)
           {
               // This is not a real authentication scheme.
               return user == password;
           }
     
           private Task<HttpResponseMessage> Unauthorized()
           {
               var response = new HttpResponseMessage(HttpStatusCode.Forbidden);
               var tsc = new TaskCompletionSource<HttpResponseMessage>();
               tsc.SetResult(response);
               return tsc.Task;
           }
       <span data-ttu-id="cc728-142">}</span><span class="sxs-lookup"><span data-stu-id="cc728-142">}</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="cc728-143">**Security Note**: The `AuthenticationTestHandler` class does not provide true authentication.</span><span class="sxs-lookup"><span data-stu-id="cc728-143">**Security Note**: The `AuthenticationTestHandler` class does not provide true authentication.</span></span> <span data-ttu-id="cc728-144">It is used only to mimic basic authentication and is not secure.</span><span class="sxs-lookup"><span data-stu-id="cc728-144">It is used only to mimic basic authentication and is not secure.</span></span> <span data-ttu-id="cc728-145">You must implement a secure authentication mechanism in your production applications and services.</span><span class="sxs-lookup"><span data-stu-id="cc728-145">You must implement a secure authentication mechanism in your production applications and services.</span></span>                
     > 
     > 
4. <span data-ttu-id="cc728-146">Add the following code at the end of the `Register` method in the **App_Start/WebApiConfig.cs** class to register the message handler:</span><span class="sxs-lookup"><span data-stu-id="cc728-146">Add the following code at the end of the `Register` method in the **App_Start/WebApiConfig.cs** class to register the message handler:</span></span>
   
        config.MessageHandlers.Add(new AuthenticationTestHandler());
5. <span data-ttu-id="cc728-147">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="cc728-147">Save your changes.</span></span>

## <a name="registering-for-notifications-using-the-webapi-backend"></a><span data-ttu-id="cc728-148">Registering for Notifications using the WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="cc728-148">Registering for Notifications using the WebAPI Backend</span></span>
<span data-ttu-id="cc728-149">In this section, we will add a new controller to the WebAPI backend to handle requests to register a user and device for notifications using the client library for notification hubs.</span><span class="sxs-lookup"><span data-stu-id="cc728-149">In this section, we will add a new controller to the WebAPI backend to handle requests to register a user and device for notifications using the client library for notification hubs.</span></span> <span data-ttu-id="cc728-150">The controller will add a user tag for the user that was authenticated and attached to the HttpContext by the `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="cc728-150">The controller will add a user tag for the user that was authenticated and attached to the HttpContext by the `AuthenticationTestHandler`.</span></span> <span data-ttu-id="cc728-151">The tag will have the string format, `"username:<actual username>"`.</span><span class="sxs-lookup"><span data-stu-id="cc728-151">The tag will have the string format, `"username:<actual username>"`.</span></span>

1. <span data-ttu-id="cc728-152">In Solution Explorer, right-click the **AppBackend** project and then click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="cc728-152">In Solution Explorer, right-click the **AppBackend** project and then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="cc728-153">On the left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in the **Search** box.</span><span class="sxs-lookup"><span data-stu-id="cc728-153">On the left-hand side, click **Online**, and search for **Microsoft.Azure.NotificationHubs** in the **Search** box.</span></span>
3. <span data-ttu-id="cc728-154">In the results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span><span class="sxs-lookup"><span data-stu-id="cc728-154">In the results list, click **Microsoft Azure Notification Hubs**, and then click **Install**.</span></span> <span data-ttu-id="cc728-155">Complete the installation, then close the NuGet package manager window.</span><span class="sxs-lookup"><span data-stu-id="cc728-155">Complete the installation, then close the NuGet package manager window.</span></span>
   
    <span data-ttu-id="cc728-156">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span><span class="sxs-lookup"><span data-stu-id="cc728-156">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="cc728-157">We will now create a new class file that represents the connection with notification hub used to send notifications.</span><span class="sxs-lookup"><span data-stu-id="cc728-157">We will now create a new class file that represents the connection with notification hub used to send notifications.</span></span> <span data-ttu-id="cc728-158">In the Solution Explorer, right-click the **Models** folder, click **Add**, then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="cc728-158">In the Solution Explorer, right-click the **Models** folder, click **Add**, then click **Class**.</span></span> <span data-ttu-id="cc728-159">Name the new class **Notifications.cs**, then click **Add** to generate the class.</span><span class="sxs-lookup"><span data-stu-id="cc728-159">Name the new class **Notifications.cs**, then click **Add** to generate the class.</span></span> 
   
    ![][B6]
5. <span data-ttu-id="cc728-160">In Notifications.cs, add the following `using` statement at the top of the file:</span><span class="sxs-lookup"><span data-stu-id="cc728-160">In Notifications.cs, add the following `using` statement at the top of the file:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
6. <span data-ttu-id="cc728-161">Replace the `Notifications` class definition with the following and make sure to replace the two placeholders with the connection string (with full access) for your notification hub, and the hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span><span class="sxs-lookup"><span data-stu-id="cc728-161">Replace the `Notifications` class definition with the following and make sure to replace the two placeholders with the connection string (with full access) for your notification hub, and the hub name (available at [Azure Classic Portal](http://manage.windowsazure.com)):</span></span>
   
        public class Notifications
        {
            public static Notifications Instance = new Notifications();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                Hub = NotificationHubClient.CreateClientFromConnectionString("<your hub's DefaultFullSharedAccessSignature>", 
                                                                             "<hub name>");
            }
        }
7. <span data-ttu-id="cc728-162">Next we will create a new controller named **RegisterController**.</span><span class="sxs-lookup"><span data-stu-id="cc728-162">Next we will create a new controller named **RegisterController**.</span></span> <span data-ttu-id="cc728-163">In Solution Explorer, right-click the **Controllers** folder, then click **Add**, then click **Controller**.</span><span class="sxs-lookup"><span data-stu-id="cc728-163">In Solution Explorer, right-click the **Controllers** folder, then click **Add**, then click **Controller**.</span></span> <span data-ttu-id="cc728-164">Click the **Web API 2 Controller -- Empty** item, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="cc728-164">Click the **Web API 2 Controller -- Empty** item, and then click **Add**.</span></span> <span data-ttu-id="cc728-165">Name the new class **RegisterController**, and then click **Add** again to generate the controller.</span><span class="sxs-lookup"><span data-stu-id="cc728-165">Name the new class **RegisterController**, and then click **Add** again to generate the controller.</span></span>
   
    ![][B7]
   
    ![][B8]
8. <span data-ttu-id="cc728-166">In RegisterController.cs, add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="cc728-166">In RegisterController.cs, add the following `using` statements:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.NotificationHubs.Messaging;
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
9. <span data-ttu-id="cc728-167">Add the following code inside the `RegisterController` class definition.</span><span class="sxs-lookup"><span data-stu-id="cc728-167">Add the following code inside the `RegisterController` class definition.</span></span> <span data-ttu-id="cc728-168">Note that in this code, we add a user tag for the user this is attached to the HttpContext.</span><span class="sxs-lookup"><span data-stu-id="cc728-168">Note that in this code, we add a user tag for the user this is attached to the HttpContext.</span></span> <span data-ttu-id="cc728-169">The user was authenticated and attached to the HttpContext by the message filter we added, `AuthenticationTestHandler`.</span><span class="sxs-lookup"><span data-stu-id="cc728-169">The user was authenticated and attached to the HttpContext by the message filter we added, `AuthenticationTestHandler`.</span></span> <span data-ttu-id="cc728-170">You can also add optional checks to verify that the user has rights to register for the requested tags.</span><span class="sxs-lookup"><span data-stu-id="cc728-170">You can also add optional checks to verify that the user has rights to register for the requested tags.</span></span>
   
        private NotificationHubClient hub;
   
        public RegisterController()
        {
            hub = Notifications.Instance.Hub;
        }
   
        public class DeviceRegistration
        {
            public string Platform { get; set; }
            public string Handle { get; set; }
            public string[] Tags { get; set; }
        }
   
        // POST api/register
        // This creates a registration id
        public async Task<string> Post(string handle = null)
        {
            string newRegistrationId = null;
   
            // make sure there are no existing registrations for this push handle (used for iOS and Android)
            if (handle != null)
            {
                var registrations = await hub.GetRegistrationsByChannelAsync(handle, 100);
   
                foreach (RegistrationDescription registration in registrations)
                {
                    if (newRegistrationId == null)
                    {
                        newRegistrationId = registration.RegistrationId;
                    }
                    else
                    {
                        await hub.DeleteRegistrationAsync(registration);
                    }
                }
            }
   
            if (newRegistrationId == null) 
                newRegistrationId = await hub.CreateRegistrationIdAsync();
   
            return newRegistrationId;
        }
   
        // PUT api/register/5
        // This creates or updates a registration (with provided channelURI) at the specified id
        public async Task<HttpResponseMessage> Put(string id, DeviceRegistration deviceUpdate)
        {
            RegistrationDescription registration = null;
            switch (deviceUpdate.Platform)
            {
                case "mpns":
                    registration = new MpnsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "wns":
                    registration = new WindowsRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "apns":
                    registration = new AppleRegistrationDescription(deviceUpdate.Handle);
                    break;
                case "gcm":
                    registration = new GcmRegistrationDescription(deviceUpdate.Handle);
                    break;
                default:
                    throw new HttpResponseException(HttpStatusCode.BadRequest);
            }
   
            registration.RegistrationId = id;
            var username = HttpContext.Current.User.Identity.Name;
   
            // add check if user is allowed to add these tags
            registration.Tags = new HashSet<string>(deviceUpdate.Tags);
            registration.Tags.Add("username:" + username);
   
            try
            {
                await hub.CreateOrUpdateRegistrationAsync(registration);
            }
            catch (MessagingException e)
            {
                ReturnGoneIfHubResponseIsGone(e);
            }
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        // DELETE api/register/5
        public async Task<HttpResponseMessage> Delete(string id)
        {
            await hub.DeleteRegistrationAsync(id);
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
        private static void ReturnGoneIfHubResponseIsGone(MessagingException e)
        {
            var webex = e.InnerException as WebException;
            if (webex.Status == WebExceptionStatus.ProtocolError)
            {
                var response = (HttpWebResponse)webex.Response;
                if (response.StatusCode == HttpStatusCode.Gone)
                    throw new HttpRequestException(HttpStatusCode.Gone.ToString());
            }
        }
10. <span data-ttu-id="cc728-171">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="cc728-171">Save your changes.</span></span>

## <a name="sending-notifications-from-the-webapi-backend"></a><span data-ttu-id="cc728-172">Sending Notifications from the WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="cc728-172">Sending Notifications from the WebAPI Backend</span></span>
<span data-ttu-id="cc728-173">In this section you add a new controller that exposes a way for client devices to send a notification based on the username tag using Azure Notification Hubs Service Management Library in the ASP.NET WebAPI backend.</span><span class="sxs-lookup"><span data-stu-id="cc728-173">In this section you add a new controller that exposes a way for client devices to send a notification based on the username tag using Azure Notification Hubs Service Management Library in the ASP.NET WebAPI backend.</span></span>

1. <span data-ttu-id="cc728-174">Create another new controller named **NotificationsController**.</span><span class="sxs-lookup"><span data-stu-id="cc728-174">Create another new controller named **NotificationsController**.</span></span> <span data-ttu-id="cc728-175">Create it the same way you created the **RegisterController** in the previous section.</span><span class="sxs-lookup"><span data-stu-id="cc728-175">Create it the same way you created the **RegisterController** in the previous section.</span></span>
2. <span data-ttu-id="cc728-176">In NotificationsController.cs, add the following `using` statements:</span><span class="sxs-lookup"><span data-stu-id="cc728-176">In NotificationsController.cs, add the following `using` statements:</span></span>
   
        using AppBackend.Models;
        using System.Threading.Tasks;
        using System.Web;
3. <span data-ttu-id="cc728-177">Add the following method to the **NotificationsController** class.</span><span class="sxs-lookup"><span data-stu-id="cc728-177">Add the following method to the **NotificationsController** class.</span></span>
   
    <span data-ttu-id="cc728-178">This code send a notification type based on the Platform Notification Service (PNS) `pns` parameter.</span><span class="sxs-lookup"><span data-stu-id="cc728-178">This code send a notification type based on the Platform Notification Service (PNS) `pns` parameter.</span></span> <span data-ttu-id="cc728-179">The value of `to_tag` is used to set the *username* tag on the message.</span><span class="sxs-lookup"><span data-stu-id="cc728-179">The value of `to_tag` is used to set the *username* tag on the message.</span></span> <span data-ttu-id="cc728-180">This tag must match a username tag of an active notification hub registration.</span><span class="sxs-lookup"><span data-stu-id="cc728-180">This tag must match a username tag of an active notification hub registration.</span></span> <span data-ttu-id="cc728-181">The notification message is pulled from the body of the POST request and formatted for the target PNS.</span><span class="sxs-lookup"><span data-stu-id="cc728-181">The notification message is pulled from the body of the POST request and formatted for the target PNS.</span></span> 
   
    <span data-ttu-id="cc728-182">Depending on the Platform Notification Service (PNS) that your supported devices use to receive notifications, different notifications are supported using different formats.</span><span class="sxs-lookup"><span data-stu-id="cc728-182">Depending on the Platform Notification Service (PNS) that your supported devices use to receive notifications, different notifications are supported using different formats.</span></span> <span data-ttu-id="cc728-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span><span class="sxs-lookup"><span data-stu-id="cc728-183">For example on Windows devices, you could use a [toast notification with WNS](https://msdn.microsoft.com/library/windows/apps/br230849.aspx) that isn't directly supported by another PNS.</span></span> <span data-ttu-id="cc728-184">So your backend would need to format the notification into a supported notification for the PNS of devices you plan to support.</span><span class="sxs-lookup"><span data-stu-id="cc728-184">So your backend would need to format the notification into a supported notification for the PNS of devices you plan to support.</span></span> <span data-ttu-id="cc728-185">Then use the appropriate send API on the [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span><span class="sxs-lookup"><span data-stu-id="cc728-185">Then use the appropriate send API on the [NotificationHubClient class](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.notificationhubclient_methods.aspx)</span></span>
   
        public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag)
        {
            var user = HttpContext.Current.User.Identity.Name;
            string[] userTag = new string[2];
            userTag[0] = "username:" + to_tag;
            userTag[1] = "from:" + user;
   
            Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;
            HttpStatusCode ret = HttpStatusCode.InternalServerError;
   
            switch (pns.ToLower())
            {
                case "wns":
                    // Windows 8.1 / Windows Phone 8.1
                    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" + 
                                "From " + user + ": " + message + "</text></binding></visual></toast>";
                    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
                    break;
                case "apns":
                    // iOS
                    var alert = "{\"aps\":{\"alert\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(alert, userTag);
                    break;
                case "gcm":
                    // Android
                    var notif = "{ \"data\" : {\"message\":\"" + "From " + user + ": " + message + "\"}}";
                    outcome = await Notifications.Instance.Hub.SendGcmNativeNotificationAsync(notif, userTag);
                    break;
            }
   
            if (outcome != null)
            {
                if (!((outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Abandoned) ||
                    (outcome.State == Microsoft.Azure.NotificationHubs.NotificationOutcomeState.Unknown)))
                {
                    ret = HttpStatusCode.OK;
                }
            }
   
            return Request.CreateResponse(ret);
        }
4. <span data-ttu-id="cc728-186">Press **F5** to run the application and to ensure the accuracy of your work so far.</span><span class="sxs-lookup"><span data-stu-id="cc728-186">Press **F5** to run the application and to ensure the accuracy of your work so far.</span></span> <span data-ttu-id="cc728-187">The app should launch a web browser and display the ASP.NET home page.</span><span class="sxs-lookup"><span data-stu-id="cc728-187">The app should launch a web browser and display the ASP.NET home page.</span></span> 

## <a name="publish-the-new-webapi-backend"></a><span data-ttu-id="cc728-188">Publish the new WebAPI Backend</span><span class="sxs-lookup"><span data-stu-id="cc728-188">Publish the new WebAPI Backend</span></span>
1. <span data-ttu-id="cc728-189">Now we will deploy this app to an Azure Website in order to make it accessible from all devices.</span><span class="sxs-lookup"><span data-stu-id="cc728-189">Now we will deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="cc728-190">Right-click on the **AppBackend** project and select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="cc728-190">Right-click on the **AppBackend** project and select **Publish**.</span></span>
2. <span data-ttu-id="cc728-191">Select **Microsoft Azure Web Apps** as your publish target.</span><span class="sxs-lookup"><span data-stu-id="cc728-191">Select **Microsoft Azure Web Apps** as your publish target.</span></span>
   
    ![][B15]
3. <span data-ttu-id="cc728-192">Log in with your Azure account and select an existing or new Web App.</span><span class="sxs-lookup"><span data-stu-id="cc728-192">Log in with your Azure account and select an existing or new Web App.</span></span>
   
    ![][B16]
4. <span data-ttu-id="cc728-193">Make a note of the **destination URL** property in the **Connection** tab. We will refer to this URL as your *backend endpoint* later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="cc728-193">Make a note of the **destination URL** property in the **Connection** tab. We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="cc728-194">Click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="cc728-194">Click **Publish**.</span></span>
   
    ![][B18]

[B1]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push1.png
[B2]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push2.png
[B3]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push3.png
[B4]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push4.png
[B5]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push5.png
[B6]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push6.png
[B7]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push7.png
[B8]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push8.png
[B14]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-secure-push14.png
[B15]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users15.PNG
[B16]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users16.PNG
[B18]: https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/notification-hubs-aspnet-backend-notifyusers/notification-hubs-notify-users18.PNG












