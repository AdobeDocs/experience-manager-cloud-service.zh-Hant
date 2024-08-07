---
title: 授權儀表板
description: Cloud Manager 提供了一個儀表板，用於輕鬆查看您的組織或租用戶可用的 AEMaaCS 產品權利。
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: eae5c75e1bf4f7201fe2c01d08737d36489ca3e4
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 31%

---


# 授權儀表板 {#license-dashboard}

Cloud Manager 提供了一個儀表板，用於輕鬆查看您的組織或租用戶可用的 AEMaaCS 產品權利。

>[!IMPORTANT]
>
>授權儀表板僅適用於AEM as a Cloud Service計畫。 [AMS程式](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/introduction)未包含在授權儀表板中。
>
>若要判斷您的程式具有的服務型別（AMS或AEMaaCS），請參閱檔案[瀏覽Cloud Manager UI。](/help/implementing/cloud-manager/navigation.md#program-cards)

## 概觀 {#overview}

Cloud Manager 授權儀表板提供對以下資訊的輕鬆存取：

1. 您可在所有程式中取得解決方案權益，包括已使用的和可用的專案
1. Sites 解決方案按月趨勢的內容請求消耗指標

## 使用授權儀表板 {#using-dashboard}

要存取您的授權儀表板，請按照以下步驟操作。

>[!NOTE]
>
>必須由具有&#x200B;**業主**&#x200B;角色的使用者登入才能檢視授權儀表板。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。
1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」主控台上，點選或按一下「[Cloud Manager標題」上的「漢堡選單」按鈕。](/help/implementing/cloud-manager/navigation.md#cloud-manager-header)這會顯示標籤。
1. 點選或按一下標籤中的&#x200B;**授權**&#x200B;選項。

![授權儀表板](assets/license-dashboard.png)

儀表板分為三個部分，向您展示：

* **解決方案**- 本節總結了您已獲得許可的解決方案，例如 Sites 或Assets。
* **附加元件** - 本節總結了您可用的授權解決方案的哪些附加元件。
* **其他權益** — 此區段總結列出哪些沙箱和開發環境，以及可在您的租使用者內使用的其他權益。

每個區段都總結了可用的內容及其使用方式（如果有的話）。 目前僅顯示Sites和Assets解決方案，即使租使用者中存在其他解決方案。

* **狀態**&#x200B;欄顯示未使用的權利數量與租使用者可用的權利總數。
* 這&#x200B;**配置在**&#x200B;清單示已套用解決方案權利的計畫。
   * 僅當已建立生產環境或已存在生產環境且已在其上執行更新管道時，才認為權利被使用。
   * 欄中只列出有限數目的程式，其餘則以`+x`專案表示。
   * 將滑鼠停留在快顯視窗的`+x`專案上，以顯示所有程式的詳細資料。
* **使用狀況**&#x200B;欄顯示&#x200B;**[檢視使用狀況詳細資料](#view-usage-details)**&#x200B;按鈕，以顯示解決方案的使用狀況統計資料。

>[!TIP]
>
>若要瞭解如何透過Admin Console管理整個組織的Adobe權益，請參閱[Admin Console概觀](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)。

## 檢視使用詳細資料 {#view-usage-details}

**檢視使用詳細資料**&#x200B;按鈕可讓您存取所選解決方案的&#x200B;**使用詳細資料**&#x200B;視窗。 此視窗提供詳細的劃分，包括顯示解決方案使用情況的圖表。 如何測量此使用方式取決於選擇的解決方案。

### 網站使用細節 {#sites-usage-details}

**Sites使用詳細資料**&#x200B;視窗會顯示圖表，提供您根據[內容要求使用Sites授權的概觀。](#what-is-a-content-request)

![網站使用狀況詳細資料視窗](assets/sites-usage-details.png)

視窗左側會顯示圓形圖，顯示在&#x200B;**檢視合約年度**&#x200B;下拉式清單中所選合約年度的合約明細。

視窗右側會顯示區域圖，其中顯示所選合約年度內一段時間內依方案劃分的使用量。 游標暫留會顯示快顯視窗，其中顯示所選時間點的每個方案的詳細資料。

### Assets使用詳細資料 {#assets-usage-details}

**Assets使用詳細資料**&#x200B;視窗顯示的圖表會根據[儲存空間](#storage)和[標準使用者，提供您Assets授權使用情形的概觀。](#standard-users)選取適當的索引標籤以在檢視之間切換。

對於儲存和標準使用者檢視，您可以使用&#x200B;**環境型別**&#x200B;下拉式清單，在生產、中繼和開發環境之間切換檢視。

#### 儲存空間 {#storage}

![儲存裝置的Assets使用量詳細資料視窗](assets/assets-usage-details-storage.png)

視窗左側會顯示圓形圖，顯示在&#x200B;**檢視合約年度**&#x200B;下拉式清單中所選合約年度的合約明細。

視窗右側會顯示區域圖，其中顯示所選合約年度內一段時間內依方案劃分的使用量。 游標暫留會顯示快顯視窗，其中顯示所選時間點的每個方案的詳細資料。

#### 標準使用者 {#standard-users}

![標準使用者的Assets使用詳細資訊視窗](assets/assets-usage-details-standard-users.png)

視窗左側會顯示圓形圖，顯示在&#x200B;**檢視合約年度**&#x200B;下拉式清單中所選合約年度的合約明細。

視窗右側會顯示區域圖，其中顯示所選合約年度內一段時間內依方案劃分的使用量。 游標暫留會顯示快顯視窗，其中顯示所選時間點的每個方案的詳細資料。

## 常見問答 {#faq}

### 什麼是內容請求？ {#what-is-a-content-request}

內容請求是進入AEM Sites或任何客戶提供的快取系統（例如內容傳遞網路）的請求，以HTML格式作為頁面檢視或JSON格式作為API呼叫傳遞內容或資料。

每次頁面查看或每五個 API 調用計算一個內容請求，在接收內容請求的第一個緩存系統的入口處測量。內容請求僅計入生產環境。

內容請求會排除僅為了提供產品和服務而由Adobe或其代表發起的請求或活動。 Adobe 識別的來自與常見搜索引擎和社交媒體服務相關的機器人、爬蟲和蜘蛛的使用者代理流量也被排除在外。

另請參閱[瞭解Cloud Service內容要求](/help/implementing/cloud-manager/content-requests.md)。

### Adobe Experience Manager 如何衡量內容請求？ {#how-are-content-requests-measured}

內容請求在 AEM as a Cloud Service 的邊緣伺服器進行追蹤。原始流量不計入內容請求。AEM as a Cloud Service 內建的 CDN 可跟踪有效的 HTML 和 JSON 請求。

AEM 還制定了排除知名機器人的規則，包括定期存取該網站以刷新其搜索索引或服務的知名服務。

另請參閱[瞭解Cloud Service內容要求](/help/implementing/cloud-manager/content-requests.md)。

### 為什麼我的 Analytics 報告顯示的結果與 AEM 內容請求不同？ {#why-are-reports-different}

內容請求可能與組織的Analytics報告工具不同。 如需詳細資訊，請參閱[瞭解Cloud Service內容要求](/help/implementing/cloud-manager/content-requests.md)。

### 如果我想了解更多有關我的內容請求量的資訊呢? {#current-request-volumes}

如果您想進一步了解授權儀表板中顯示的內容請求量，您的 Adobe 團隊可以提供一份報告，顯示內容請求的主要數量驅動因素。請聯絡您的Adobe團隊或Adobe客戶支援，以請求最高使用量報告。

### 如果我使用自己的 CDN 怎麼辦？ {#using-own-cdn}

授權儀表板只會顯示Cloud ServiceCDN追蹤的資料。 如果您選擇使用自己的CDN (BYOCDN)，請按照合約中的規定每年向Adobe報告您的內容請求量。
