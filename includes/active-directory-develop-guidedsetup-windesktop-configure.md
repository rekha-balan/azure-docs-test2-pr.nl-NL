
## <a name="register-your-application"></a><span data-ttu-id="2f068-101">Register your application</span><span class="sxs-lookup"><span data-stu-id="2f068-101">Register your application</span></span>
<span data-ttu-id="2f068-102">You can register your application in either of two ways.</span><span class="sxs-lookup"><span data-stu-id="2f068-102">You can register your application in either of two ways.</span></span>

### <a name="option-1-express-mode"></a><span data-ttu-id="2f068-103">Option 1: Express mode</span><span class="sxs-lookup"><span data-stu-id="2f068-103">Option 1: Express mode</span></span>
<span data-ttu-id="2f068-104">You can quickly register your application by doing the following:</span><span class="sxs-lookup"><span data-stu-id="2f068-104">You can quickly register your application by doing the following:</span></span>
1. <span data-ttu-id="2f068-105">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure).</span><span class="sxs-lookup"><span data-stu-id="2f068-105">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure).</span></span>

2. <span data-ttu-id="2f068-106">Select **Add an app**.</span><span class="sxs-lookup"><span data-stu-id="2f068-106">Select **Add an app**.</span></span>

3. <span data-ttu-id="2f068-107">In the **Application Name** box, enter a name for your application.</span><span class="sxs-lookup"><span data-stu-id="2f068-107">In the **Application Name** box, enter a name for your application.</span></span>

4. <span data-ttu-id="2f068-108">Ensure that the **Guided Setup** check box is selected, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="2f068-108">Ensure that the **Guided Setup** check box is selected, and then select **Create**.</span></span>

5. <span data-ttu-id="2f068-109">Follow the instructions for obtaining the application ID, and paste it into your code.</span><span class="sxs-lookup"><span data-stu-id="2f068-109">Follow the instructions for obtaining the application ID, and paste it into your code.</span></span>

### <a name="option-2-advanced-mode"></a><span data-ttu-id="2f068-110">Option 2: Advanced mode</span><span class="sxs-lookup"><span data-stu-id="2f068-110">Option 2: Advanced mode</span></span>
<span data-ttu-id="2f068-111">To register your application and add your application registration information to your solution, do the following:</span><span class="sxs-lookup"><span data-stu-id="2f068-111">To register your application and add your application registration information to your solution, do the following:</span></span>
1. <span data-ttu-id="2f068-112">If you haven't already registered your application, go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app).</span><span class="sxs-lookup"><span data-stu-id="2f068-112">If you haven't already registered your application, go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app).</span></span>

2. <span data-ttu-id="2f068-113">Select **Add an app**.</span><span class="sxs-lookup"><span data-stu-id="2f068-113">Select **Add an app**.</span></span>

3. <span data-ttu-id="2f068-114">In the **Application Name** box, enter a name for your application.</span><span class="sxs-lookup"><span data-stu-id="2f068-114">In the **Application Name** box, enter a name for your application.</span></span> 

4. <span data-ttu-id="2f068-115">Ensure that the **Guided Setup** check box is cleared, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="2f068-115">Ensure that the **Guided Setup** check box is cleared, and then select **Create**.</span></span>

5. <span data-ttu-id="2f068-116">Select **Add Platform**, select **Native Application**, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="2f068-116">Select **Add Platform**, select **Native Application**, and then select **Save**.</span></span>

6. <span data-ttu-id="2f068-117">In the **Application ID** box, copy the GUID.</span><span class="sxs-lookup"><span data-stu-id="2f068-117">In the **Application ID** box, copy the GUID.</span></span>

7. <span data-ttu-id="2f068-118">Go to Visual Studio, open the *App.xaml.cs* file, and then replace `your_client_id_here` with the application ID that you just registered and copied.</span><span class="sxs-lookup"><span data-stu-id="2f068-118">Go to Visual Studio, open the *App.xaml.cs* file, and then replace `your_client_id_here` with the application ID that you just registered and copied.</span></span>

    ```csharp
    private static string ClientId = "your_application_id_here";
    ```
