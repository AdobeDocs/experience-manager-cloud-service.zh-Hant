---
title: Adobe Experience Manager as a Cloud Service的微前端內容片段選擇器屬性
description: 屬性可設定微前端內容片段選擇器，以搜尋、尋找及擷取您應用程式的內容片段。
role: Admin, User
exl-id: c81b5256-09fb-41ce-9581-f6d1ad316ca4
source-git-commit: 58995ae9c29d5a76b3f94de43f2bafecdaf7cf68
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 4%

---

# 內容片段選擇器 - 相關屬性 {#content-fragment-selector-related-properties}

微前端內容片段選擇器可讓您瀏覽或搜尋存放庫中的內容片段，並在您的應用程式中使用這些片段。

您可以使用以下屬性來自訂內容片段選擇器的呈現方式及其使用方式：

## 內容片段選擇器屬性 {#content-fragment-selector-properties}

| 屬性 | 類型 | 必要 | 預設 | 說明 |
|--- |--- |--- |--- |--- |
| `ref` | FragmentSelectorRef | | | 參考`ContentFragmentSelector`執行個體，允許存取提供的功能，例如`reload`。 |
| `imsToken` | 字串 | 否 | | 用於驗證的IMS權杖。 如果未提供，將起始IMS登入流程。 |
| `repoId` | 字串 | 否 | | 用於片段選擇器的存放庫ID。 提供後，選取器會自動連線至指定的存放庫，而存放庫下拉式清單會隱藏。 如果未提供，使用者可以從他們有權存取的可用存放庫清單中選取存放庫。 |
| `defaultRepoId` | 字串 | 否 | | 顯示存放庫選擇器時，預設會選取的存放庫ID。 僅在未提供`repoId`時使用。 如果設定`repoId`，則會隱藏存放庫選擇器，並忽略此值。 |
| `orgId` | 字串 | 否 | | 用於驗證的組織ID。 如果未提供，使用者可以從他們有權存取的不同組織中選擇存放庫。 如果使用者無權存取任何存放庫或組織，則不會載入內容。 |
| `locale` | 字串 | 否 | &quot;en-US&quot; | 地區設定。 |
| `env` | 字串 | 否 | | 部署環境。 檢視允許的環境名稱的`Env`型別。 |
| `filters` | Fragmentfilter | 否 | `{ folder: "/content/dam" }` | 要套用至內容片段清單的篩選器。 依預設，`/content/dam`下的片段將會顯示。 |
| `isOpen` | 布林值 | 否 | `false` | 控制選取器是開啟還是關閉的旗標。 |
| `noWrap` | 布林值 | 否 | `false` | 決定是否呈現片段選擇器而不使用包裝對話方塊。 設定為`true`時，片段選擇器會直接內嵌在父容器中。 將選取器整合至自訂配置或工作流程時相當實用。 |
| `onSelectionChange` | ({ contentFragments： `ContentFragmentSelection`， domainName？： `string`， tenantInfo？： `string`， repoId？： `string`， deliveryRepos？： `DeliveryRepository[]` }) => void | 否 | | 每當內容片段的選擇變更時，就會觸發回呼函式。 提供目前選取的片段、網域名稱、租使用者資訊、存放庫ID和傳遞存放庫。 |
| `onDismiss` | () =>無效 | 否 | | 執行解除動作時觸發的回呼函式（例如，關閉選取器）。 |
| `onSubmit` | ({ contentFragments： `ContentFragmentSelection`， domainName？： `string`， tenantInfo？： `string`， repoId？： `string`， deliveryRepos？： `DeliveryRepository[]` }) => void | 否 | | 使用者確認選取時觸發的回呼函式。 接收選取的內容片段、網域名稱、租使用者資訊、存放庫ID和傳遞存放庫。 |
| `theme` | &quot;light&quot;或&quot;dark&quot; | 否 | | 片段選擇器的主題。 預設會設定為unifiedShell環境主題。 |
| `selectionType` | 「單一」或「多個」 | 否 | `single` | 選擇型別可用於限製片段選擇器的選擇。 |
| `dialogSize` | &quot;fullscreen&quot;或&quot;fullscreenTakeover&quot; | 否 | `fullscreen` | 控制對話方塊大小的選用Prop。 |
| `runningInUnifiedShell` | 布林值 | 否 | | DestinationSelector是在UnifiedShell下執行，還是獨立執行。 |
| `readonlyFilters` | ResourceReadonlyFiltersField[] | 否 | | 唯讀篩選器套用到內容片段清單。 使用者無法移除這些篩選器。 |
| `selectedFragments` | ContentFragmentIdentifier[] | 否 | `[]` | 選擇器開啟時要預先選取的內容片段的初始選擇。 |
| `hipaaEnabled` | 布林值 | 否 | `false` | 指出是否已啟用HIPAA規範。 |
| `inventoryView` | InventoryViewType | 否 | `table` | 要用於選擇器的詳細目錄預設檢視型別。 |
| `inventoryViewToggleEnabled` | 布林值 | 否 | `false` | 表示是否啟用庫存檢視切換，讓使用者在表格檢視和格線檢視之間切換。 |

## ImsAuthProps屬性 {#imsauthprops-properties}

`ImsAuthProps`屬性定義內容片段選擇器用來取得`imsToken`的驗證資訊和流程。 藉由設定這些屬性，您可以控制驗證流程應該如何行為並註冊各種驗證事件的接聽程式。

| 屬性名稱 | 說明 |
|--- |--- |
| `imsClientId` | 代表用於驗證目的之IMS使用者端ID的字串值。 此值由Adobe提供，且為您的Adobe AEM CS組織專用。 |
| `imsScope` | 說明用於驗證的範圍。 範圍會決定應用程式對貴組織資源的存取層級。 多個範圍可以用逗號分隔。 |
| `redirectUrl` | 代表驗證後重新導向使用者的URL。 此值通常設定為應用程式目前的URL。 如果未提供`redirectUrl`，`ImsAuthService`將使用用來登入`imsClientId`的redirectUrl |
| `modalMode` | 表示驗證流程是否應該顯示在強制回應視窗（快顯視窗）中的布林值。 如果設為`true`，驗證流程會以快顯視窗顯示。 如果設為`false`，則驗證流程會以全頁重新載入顯示。<br>**注意：**&#x200B;若要獲得較好的UX，您可以在使用者停用瀏覽器快顯視窗時動態控制此值。 |
| `onImsServiceInitialized` | Adobe IMS驗證服務初始化時呼叫的回呼函式。 此函式接受一個引數`service`，此引數是代表Adobe IMS服務的物件。 如需詳細資訊，請參閱[`ImsAuthService`](#imsauthservice-ims-auth-service)。 |
| `onAccessTokenReceived` | 從Adobe IMS驗證服務收到`imsToken`時所呼叫的回呼函式。 此函式接受一個引數`imsToken`，該引數是代表存取權杖的字串。 |
| `onAccessTokenExpired` | 當存取權杖過期時所呼叫的回呼函式。 此函式通常用於觸發新的驗證流程，以取得新的存取權杖。 |
| `onErrorReceived` | 驗證期間發生錯誤時所呼叫的回呼函式。 此函式採用兩個引數：錯誤型別和錯誤訊息。 錯誤型別是代表錯誤型別的字串，而錯誤訊息是代表錯誤訊息的字串。 |

## ImsAuthService屬性 {#imsauthservice-properties}

`ImsAuthService`類別會處理內容片段選擇器的驗證流程。 其負責從Adobe IMS驗證服務取得`imsToken`。 `imsToken`用於驗證使用者並授權存取Adobe Experience Manager (AEM) CS存放庫。 ImsAuthService使用`ImsAuthProps`屬性來控制驗證流程並註冊各種驗證事件的接聽程式。 您可以使用方便的`registerContentFragmentSelectorAuthService`函式向內容片段選取器註冊`ImsAuthService`執行個體。 `ImsAuthService`類別上有以下可用函式。 不過，如果您使用`registerContentFragmentSelectorAuthService`函式，則不需要直接呼叫這些函式。

| 函式名稱 | 說明 |
|--- |--- |
| `isSignedInUser` | 判斷使用者目前是否已登入服務並據此傳回布林值。 |
| `getImsToken` | 擷取目前登入使用者的驗證`imsToken`，此驗證可用於驗證其他服務的要求，例如產生資產&#x200B;_轉譯。_ |
| `signIn` | 起始使用者的登入程式。 此函式使用`ImsAuthProps`在快顯視窗或整頁重新載入中顯示驗證。 |
| `signOut` | 將使用者登出服務，讓其驗證Token失效，並要求他們再次登入以存取受保護的資源。 叫用此函式將會重新載入目前頁面。 |
| `refreshToken` | 重新整理目前登入使用者的驗證Token，避免其到期並確保受保護資源的存取不中斷。 傳回可用於後續請求的新驗證Token。 |
