
1. <span data-ttu-id="98b1c-101">Open the shared project file MainPage.cs and add the following code snippet to the MainPage class:</span><span class="sxs-lookup"><span data-stu-id="98b1c-101">Open the shared project file MainPage.cs and add the following code snippet to the MainPage class:</span></span>
   
        // Define a member variable for storing the signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs the authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' to the name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    <span data-ttu-id="98b1c-102">This code authenticates the user with a Facebook login.</span><span class="sxs-lookup"><span data-stu-id="98b1c-102">This code authenticates the user with a Facebook login.</span></span> <span data-ttu-id="98b1c-103">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span><span class="sxs-lookup"><span data-stu-id="98b1c-103">If you are using an identity provider other than Facebook, change the value of **MobileServiceAuthenticationProvider** above to the value for your provider.</span></span>
2. <span data-ttu-id="98b1c-104">Comment-out or delete the call to the **RefreshTodoItems** method in the existing **OnNavigatedTo** method override.</span><span class="sxs-lookup"><span data-stu-id="98b1c-104">Comment-out or delete the call to the **RefreshTodoItems** method in the existing **OnNavigatedTo** method override.</span></span>
   
    <span data-ttu-id="98b1c-105">This prevents the data from being loaded before the user is authenticated.</span><span class="sxs-lookup"><span data-stu-id="98b1c-105">This prevents the data from being loaded before the user is authenticated.</span></span> <span data-ttu-id="98b1c-106">Next, you will add a **Sign in** button to the app that triggers authentication.</span><span class="sxs-lookup"><span data-stu-id="98b1c-106">Next, you will add a **Sign in** button to the app that triggers authentication.</span></span>
3. <span data-ttu-id="98b1c-107">Add the following code snippet to the MainPage class:</span><span class="sxs-lookup"><span data-stu-id="98b1c-107">Add the following code snippet to the MainPage class:</span></span>
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login the user and then load data from the mobile app.
            if (await AuthenticateAsync())
            {
                // Hide the login button and load items from the mobile app.
                ButtonLogin.Visibility = Windows.UI.Xaml.Visibility.Collapsed;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. <span data-ttu-id="98b1c-108">In the Windows Store app project, open the MainPage.xaml project file and add the following **Button** element just before the element that defines the **Save** button:</span><span class="sxs-lookup"><span data-stu-id="98b1c-108">In the Windows Store app project, open the MainPage.xaml project file and add the following **Button** element just before the element that defines the **Save** button:</span></span>
   
        <Button Name="ButtonLogin" Click="ButtonLogin_Click" 
                        Visibility="Visible">Sign in</Button>
5. <span data-ttu-id="98b1c-109">In the Windows Phone Store app project, add the following **Button** element in the **ContentPanel**, after the **TextBox** element:</span><span class="sxs-lookup"><span data-stu-id="98b1c-109">In the Windows Phone Store app project, add the following **Button** element in the **ContentPanel**, after the **TextBox** element:</span></span>
   
        <Button Grid.Row ="1" Grid.Column="1" Name="ButtonLogin" Click="ButtonLogin_Click" 
            Margin="10, 0, 0, 0" Visibility="Visible">Sign in</Button>
6. <span data-ttu-id="98b1c-110">Open the shared App.xaml.cs project file and add the following code:</span><span class="sxs-lookup"><span data-stu-id="98b1c-110">Open the shared App.xaml.cs project file and add the following code:</span></span>
   
        protected override void OnActivated(IActivatedEventArgs args)
        {
            // Windows Phone 8.1 requires you to handle the respose from the WebAuthenticationBroker.
            #if WINDOWS_PHONE_APP
            if (args.Kind == ActivationKind.WebAuthenticationBrokerContinuation)
            {
                // Completes the sign-in process started by LoginAsync.
                // Change 'MobileService' to the name of your MobileServiceClient instance. 
                App.MobileService.LoginComplete(args as WebAuthenticationBrokerContinuationEventArgs);
            }
            #endif
   
            base.OnActivated(args);
        }
   
    <span data-ttu-id="98b1c-111">If the **OnActivated** method already exists, just add the `#if...#endif` code block.</span><span class="sxs-lookup"><span data-stu-id="98b1c-111">If the **OnActivated** method already exists, just add the `#if...#endif` code block.</span></span>
7. <span data-ttu-id="98b1c-112">Press the F5 key to run the Windows Store app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span><span class="sxs-lookup"><span data-stu-id="98b1c-112">Press the F5 key to run the Windows Store app, click the **Sign in** button, and sign into the app with your chosen identity provider.</span></span> 
   
       When you are successfully logged-in, the app should run without errors, and you should be able to query your backend and make updates to data.
8. <span data-ttu-id="98b1c-113">Right-click the Windows Phone Store app project, click **Set as StartUp Project**, then repeat the previous step to verify that the Windows Phone Store app also runs correctly.</span><span class="sxs-lookup"><span data-stu-id="98b1c-113">Right-click the Windows Phone Store app project, click **Set as StartUp Project**, then repeat the previous step to verify that the Windows Phone Store app also runs correctly.</span></span>  

