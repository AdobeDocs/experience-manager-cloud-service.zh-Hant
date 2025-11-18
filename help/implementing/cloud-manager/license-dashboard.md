---
title: 授權儀表板
description: Cloud Manager 提供了一個儀表板，用於輕鬆查看您的組織或租用戶可用的 AEMaaCS 產品權利。
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: 4bebe8a3a283711a053320bfda4a8aac32096aa6
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 21%

---


# 授權儀表板 {#license-dashboard}

Cloud Manager提供了一個儀表板，用於輕鬆檢視您的組織或租使用者可用的Adobe Experience Manager as a Cloud Service (AEMaaCS)產品權利。

>[!IMPORTANT]
>
>授權儀表板僅適用於AEM as a Cloud Service計畫。 [AMS程式](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-manager/content/introduction)未包含在授權儀表板中。
>
>若要判斷您的程式具有的服務型別（AMS或AEMaaCS），請參閱[瀏覽Cloud Manager UI](/help/implementing/cloud-manager/navigation.md#program-cards)。

## 概觀 {#overview}

Cloud Manager授權儀表板可讓您輕鬆存取所有計畫中可用的解決方案權益，包括使用的數量和可用的數量。 以及Sites解決方案按月趨勢的內容請求消耗量度。

## 存取授權儀表板 {#using-dashboard}

>[!NOTE]
>
>必須由具有&#x200B;**業主**&#x200B;角色的使用者登入才能檢視授權儀表板。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。
1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，按一下![Cloud Manager標題](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg)上的[顯示功能表圖示](/help/implementing/cloud-manager/navigation.md#cloud-manager-header)。 此動作會顯示標籤。
1. 按一下索引標籤中的&#x200B;**授權**&#x200B;選項。

![授權儀表板](assets/license-dashboard.png)

儀表板分為三個部分，向您展示：

* **解決方案** — 您已授權哪些解決方案。 例如Sites、Edge Delivery Services、Assets等。

  ![解決方案清單](assets/solutions.png)

* **附加元件** — 您可用的授權解決方案的哪些附加元件。
* **其他權益** — 可在您的租使用者內使用的沙箱和開發環境及其他權益。

每個區段都總結了可用的內容及其使用方式（如果有的話）。 目前，即使租使用者中存在其他解決方案，也只會顯示Sites和Assets解決方案。

* **狀態**&#x200B;欄顯示未使用的權利數量與租使用者可用的權利總數。
* 這&#x200B;**配置在**&#x200B;清單示已套用解決方案權利的計畫。
   * 只有在建立生產環境時，才會將權益視為使用。 或者，如果存在管道，且已在其上執行更新管道。
   * 欄中只列出有限數目的程式，其餘則以`+x`專案表示。
   * 將游標暫留在`+x`專案上，即可看到包含所有程式詳細資訊的快顯視窗。
* **使用狀況**&#x200B;欄顯示&#x200B;**[檢視使用狀況詳細資料](#view-usage-details)**&#x200B;按鈕，以顯示解決方案的使用狀況統計資料。

>[!TIP]
>
>若要瞭解如何透過Admin Console管理整個組織中的Adobe權益，請參閱[Admin Console概觀](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)。

## 檢視使用情況的詳細資訊 {#view-usage-details}

<!--
The **View usage details** button gives access to the chosen solution's **Usage Details** window. This window gives a detailed breakdown including charts to show your solution's usage. How that usage is measured depends on the chosen solution. -->

Cloud Manager授權區域中的&#x200B;**檢視使用狀況詳細資料**&#x200B;按鈕提供您目前資源使用狀況的詳細劃分。 按一下就會開啟報表或控制面板，顯示與授權相關的重要量度。 <!-- ADD THIS SENTENCE IF ASSETS USAGE DETAILS GETS REINSTATED ", such as the number of users, storage consumption, or bandwidth usage, depending on the type of services you're using." -->此功能可協助您監視並確保您保持在合約的限制內，同時提供深入分析以更好地規劃資源及最佳化。

在下列情況中，**檢視使用狀況詳細資料**&#x200B;按鈕為&#x200B;*已停用* （已關閉）：

* 本解決方案不屬於您的合約，且沒有信用額度。 若存在銷退折讓，即使已沖銷所有銷退折讓，此按鈕仍可使用。
* 沒有針對該解決方案設定的Cloud Manager程式。
* 控制使用詳細資訊的功能標幟已停用。 按鈕可用之前，必須為您的組織&#x200B;*啟用* （已開啟）。
* 解決方案的使用已明確停用。 目前此情況僅適用於Edge Delivery Services。



### Sites 使用情況詳細資訊 {#sites-usage-details}

**Sites使用詳細資料**&#x200B;視窗會顯示圖表，提供您根據[內容要求](#what-is-a-content-request)的Sites授權使用概況。

![網站使用狀況詳細資料視窗](assets/sites-usage-details.png)

視窗左側會顯示圓形圖，顯示在&#x200B;**檢視合約年度**&#x200B;下拉式清單中所選合約年度的合約明細。

視窗右側會顯示區域圖，其中顯示所選合約年度內一段時間內依方案劃分的使用量。 游標暫留會顯示快顯視窗，其中顯示所選時間點的每個方案的詳細資料。

在儀表板頁面的右上角附近，您可以按一下&#x200B;**下載報表**，將其資料匯出為CSV檔案。 此下載檔案可簡化分析和共用使用趨勢的程式。

<!-- REMOVED AS PER CQDOC-21983
### Assets usage details {#assets-usage-details}

The **Assets usage details** window, presents graphs giving an overview of the usage of your Assets licenses based on [storage](#storage) and [standard users](#standard-users). Select the appropriate tab to toggle between the views.

For both storage and standard users views, you can use the **Environment Type** dropdown to toggle the view between production, stage, and development environments.

#### Storage {#storage}

![Assets usage details window for storage](assets/assets-usage-details-storage.png)

The left side of the window presents a pie chart showing the contract breakdown for the contract year selected in the **View contract year** dropdown.

The right side of the window presents an area chart showing the usage broken down by program over time for the selected contract year. A hover reveals a popup with details per program for the selected point in time.

#### Standard Users {#standard-users}

![Assets usage details window for standard-users](assets/assets-usage-details-standard-users.png)

The left side of the window presents a pie chart showing the contract breakdown for the contract year selected in the **View contract year** dropdown.

The right side of the window presents an area chart showing the usage broken down by program over time for the selected contract year. A hover reveals a popup with details per program for the selected point in time. -->

## 常見問題 {#faq}

### 什麼是內容請求？{#what-is-a-content-request}

內容請求是任何導向至AEM Sites或客戶提供的快取系統（例如內容傳遞網路）的請求。 它會擷取HTML格式的內容或資料以供頁面檢視。 或者，以JSON格式用於API呼叫。

每次頁面查看或每五個 API 調用計算一個內容請求，在接收內容請求的第一個緩存系統的入口處測量。內容請求僅計入生產環境。

內容請求會排除僅為了提供產品和服務而由或代表Adobe提出的請求或活動。 Adobe 識別的來自與常見搜索引擎和社交媒體服務相關的機器人、爬蟲和蜘蛛的使用者代理流量也被排除在外。

另請參閱[瞭解Cloud Service內容要求](/help/implementing/cloud-manager/content-requests.md)。

### Adobe Experience Manager 如何衡量內容請求？{#how-are-content-requests-measured}

內容請求在 AEM as a Cloud Service 的邊緣伺服器進行追蹤。原始流量不計入內容請求。AEM as a Cloud Service 內建的 CDN 可跟踪有效的 HTML 和 JSON 請求。

AEM 還制定了排除知名機器人的規則，包括定期存取該網站以刷新其搜索索引或服務的知名服務。

另請參閱[瞭解Cloud Service內容請求](/help/implementing/cloud-manager/content-requests.md)。

### 為什麼我的Analytics報表顯示的結果與AEM內容請求不同？{#why-are-reports-different}

內容請求可能與組織的Analytics報告工具不同。 如需詳細資訊，請參閱[瞭解Cloud Service內容要求](/help/implementing/cloud-manager/content-requests.md)。

### 如果我想了解更多有關我的內容請求量的資訊呢?{#current-request-volumes}

如果您想進一步瞭解授權儀表板中顯示的內容請求量，您的Adobe團隊可以提供一份報告，顯示內容請求的主要數量驅動因素。 請聯絡您的Adobe團隊或Adobe客戶支援，以請求最高使用量報告。

### 如果我使用自己的 CDN 怎麼辦？{#using-own-cdn}

授權儀表板只會顯示Cloud Service CDN追蹤的資料。 如果您選擇使用自己的CDN (BYOCDN)，請按照合約中的規定每年向Adobe報告您的內容請求量。


