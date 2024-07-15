---
title: 授權儀表板
description: Cloud Manager 提供了一個儀表板，用於輕鬆查看您的組織或租用戶可用的 AEMaaCS 產品權利。
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 58%

---

# 授權儀表板 {#license-dashboard}

Cloud Manager 提供了一個儀表板，用於輕鬆查看您的組織或租用戶可用的 AEMaaCS 產品權利。

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

1. 在&#x200B;**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**&#x200B;主控台上，切換至&#x200B;**授權**&#x200B;標籤。

![授權儀表板](assets/license-dashboard.png)

儀表板分為三個部分，向您展示：

* **解決方案**- 本節總結了您已獲得許可的解決方案，例如 Sites 或Assets。
* **附加元件** - 本節總結了您可用的授權解決方案的哪些附加元件。
* **沙箱和開發環境**- 本節總結了您可以使用的環境。

每個區段都總結了可用的內容及其使用方式（如果有的話）。 當前僅顯示 Sites 解決方案，即使租用戶中存在其他解決方案。

* **狀態**&#x200B;欄顯示未使用的權利數量與租使用者可用的權利總數。
* 這&#x200B;**配置在**&#x200B;清單示已套用解決方案權利的計畫。
   * 僅當已建立生產環境或已存在生產環境且已在其上執行更新管道時，才認為權利被使用。
* 此&#x200B;**使用方式**&#x200B;按一下時，資料行將過去 12 個月內消耗的內容請求顯示為圖表。

>[!TIP]
>
>若要瞭解如何透過Admin Console管理整個組織的Adobe權益，請參閱[Admin Console概觀](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)。

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
