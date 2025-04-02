---
title: Adobe Experience Manager as a Cloud Service的微前端內容片段選擇器屬性
description: 屬性可設定微前端內容片段選擇器，以搜尋、尋找及擷取您應用程式的內容片段。
role: Admin, User
exl-id: c81b5256-09fb-41ce-9581-f6d1ad316ca4
source-git-commit: a3d8961b6006903c42d983c82debb63ce8abe9ad
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 3%

---

# 內容片段選擇器 — 相關屬性 {#content-fragment-selector-related-properties}

微前端內容片段選擇器可讓您瀏覽或搜尋存放庫中的內容片段，並在您的應用程式中使用這些片段。

您可以使用以下屬性來自訂內容片段選擇器的呈現方式及其使用方式：

## 內容片段選擇器屬性 {#content-fragment-selector-properties}

| 屬性 | 類型 | 必要 | 預設 | 說明 |
|--- |--- |--- |--- |--- |
| `imsToken` | 字串 | 否 | | 用於驗證的IMS權杖。 |
| `repoId` | 字串 | 否 | | 用於驗證的存放庫ID。 |
| `orgId` | 字串 | 是 | | 用於驗證的組織ID。 |
| `locale` | 字串 | 否 | | 地區設定資料。 |
| `env` | 環境 | 否 | | 內容片段選擇器部署環境。 |
| `filters` | Fragmentfilter | 否 | | 要套用於內容片段清單的篩選器。 依預設，`/content/dam`下的片段將會顯示。 預設值： `{ folder: "/content/dam" }` |
| `isOpen` | 布林值 | 是 | `false` | 此旗標可觸發開啟或關閉選取器。 |
| `onDismiss` | () =>無效 | 是 | | 選取&#x200B;**解除**&#x200B;時要呼叫的函式。 |
| `onSubmit` | ({ contentFragments： `{id: string, path: string}[]`， domainNames： `string[]` }) => void | 是 | | 選取一或多個內容片段後使用&#x200B;**Select**&#x200B;時要呼叫的函式。 <br><br>函式將接收：<br><ul><li> 具有`id`和`path`欄位的所選內容片段</li><li>與存放庫的計畫識別碼和環境識別碼相關的網域名稱，其狀態為`ready`和`tier`發佈</li></ul><br>如果沒有網域名稱，則會使用Publish執行個體做為遞補網域。 |
| `theme` | &quot;light&quot;或&quot;dark&quot; | 否 | | 內容片段選擇器的主題。 預設主題已設定為UnifiedShell環境的主題。 |
| `selectionType` | 「單一」或「多個」 | 否 | `single` | 可用來限制FragmentSelector選取範圍的選取型別。 |
| `dialogSize` | &quot;fullscreen&quot;或&quot;fullscreenTakeover&quot; | 否 | `fullscreen` | 控制對話方塊大小的選用屬性。 |
| `waitForImsToken` | 布林值 | 否 | `false` | 表示內容片段選擇器是否在SUSI流程的內容中呈現，且需要等待`imsToken`準備就緒。 |
| `imsAuthInfo` | ImsAuthInfo | 否 | | 包含登入使用者的IMS驗證資訊的物件。 |
| `runningInUnifiedShell` | 布林值 | 否 | | 指出內容片段選擇器是在UnifiedShell下執行，還是獨立執行。 |
| `readonlyFilters` | ResourceReadonlyFiltersField | 否 | | 可應用於內容清單且無法移除的唯讀篩選器。 |

## ImsAuthProps屬性 {#imsauthprops-properties}

`ImsAuthProps`屬性定義內容片段選擇器用來取得`imsToken`的驗證資訊和流程。 藉由設定這些屬性，您可以控制驗證流程應該如何行為並註冊各種驗證事件的接聽程式。

| 屬性名稱 | 描述 |
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

| 函式名稱 | 描述 |
|--- |--- |
| `isSignedInUser` | 判斷使用者目前是否已登入服務並據此傳回布林值。 |
| `getImsToken` | 擷取目前登入使用者的驗證`imsToken`，此驗證可用於驗證其他服務的要求，例如產生資產&#x200B;_轉譯。_ |
| `signIn` | 起始使用者的登入程式。 此函式使用`ImsAuthProps`在快顯視窗或整頁重新載入中顯示驗證。 |
| `signOut` | 將使用者登出服務，讓其驗證Token失效，並要求他們再次登入以存取受保護的資源。 叫用此函式將會重新載入目前頁面。 |
| `refreshToken` | 重新整理目前登入使用者的驗證Token，避免其到期並確保受保護資源的存取不中斷。 傳回可用於後續請求的新驗證Token。 |
