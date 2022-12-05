---
title: 授權儀表板
description: Cloud Manager 提供了一個儀表板，用於輕鬆查看您的組織或租使用者可用的 AEMaaCS 產品權利。
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
source-git-commit: b5078c849c9fa088546f5df1fcbef1dec59f3cdb
workflow-type: ht
source-wordcount: '876'
ht-degree: 100%

---

# 授權儀表板 {#license-dashboard}

Cloud Manager 提供了一個儀表板，用於輕鬆查看您的組織或租使用者可用的 AEMaaCS 產品權利。

## 概觀 {#overview}

Cloud Manager 授權儀表板提供對以下資訊的輕鬆存取：

1. 您可以在所有程序中使用的解決方案權利，包括已使用的和可用的
1. Sites 解決方案按月趨勢的內容請求消耗指標

## 使用授權儀表板 {#using-dashboard}

要存取您的授權儀表板，請按照以下步驟操作。

>[!NOTE]
>
>必須由具有&#x200B;**業主**&#x200B;角色的使用者登入才能檢視和儀表板的授權。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在產品概覽頁面上，切換到&#x200B;**執照**&#x200B;標籤。

![授權儀表板](assets/license-dashboard.png)

儀表板分為三個部分，向您展示：

* **解決方案**- 本節總結了您已獲得許可的解決方案，例如 Sites 或Assets。
* **附加元件** - 本節總結了您可用的授權解決方案的哪些附加元件。
* **沙箱和開發環境**- 本節總結了您可以使用的環境。

每個部分都總結了可用的內容以及當前的使用方式 (如果有的話)。當前僅顯示 Sites 解決方案，即使租使用者中存在其他解決方案。

* 這&#x200B;**地位**&#x200B;列顯示未使用的權利數量與租使用者可用的權利總數。
* 這&#x200B;**配置在**&#x200B;清單示已應用解決方案權利的程序。
   * 僅當已建立生產環境或已存在生產環境且已在其上執行更新管道時，才認為權利被使用。
* 此&#x200B;**使用方式**&#x200B;點擊時，資料行將過去 12 個月內消耗的內容請求顯示為圖表。

>[!TIP]
>
>參考[Admin Console 總覽](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)了解如何透過 Admin Console 在整個組織中管理您的 Adobe 權利。

## 常見問答 {#faq}

### 什麼是內容請求？ {#what-is-a-content-request}

內容請求是進入 AEM Sites 或任何客戶提供的快取系統 (例如內容傳遞網路) 的請求，以 HTML 格式作為頁面檢視或 JSON 格式作為 API 呼叫以傳遞內容或資料。

每次頁面查看或每五個 API 調用計算一個內容請求，在接收內容請求的第一個緩存系統的入口處測量。內容請求僅計入生產環境。

內容請求不包括由 Adobe 或代表 Adobe 發起的僅用於提供產品和服務的請求或活動。Adobe 識別的來自與常見搜索引擎和社交媒體服務相關的機器人、爬蟲和蜘蛛的使用者代理流量也被排除在外。

### Adobe Experience Manager 如何衡量內容請求？ {#how-are-content-requests-measured}

內容請求在 AEM as a Cloud Service 的邊緣伺服器進行追蹤。原始流量不計入內容請求。AEM as a Cloud Service 內建的 CDN 可跟踪有效的 HTML 和 JSON 請求。

AEM 還制定了排除知名機器人的規則，包括定期存取該網站以刷新其搜索索引或服務的知名服務。

### 為什麼我的 Analytics 報告顯示的結果與 AEM 內容請求不同？ {#why-are-reports-different}

內容請求將與組織的分析報告工具有所不同，如本表中所述。

| 差異原因 | 解釋 |
|---|---|
| 標記 | 作為 AEM 內容請求跟踪的所有頁面可能會或可能不會使用 Analytics 跟踪進行標記。作為 AEM 內容請求跟踪的所有 API 調用不會被組織的分析工具標記。<br>頁面或 API 調用可能會被標記為跟踪操作或只是唯一的頁面視圖而不是所有視圖。 |
| Tag Management 規則 | Tag Management 規則設定可能會導致頁面上的各種數據收集配置，從而導致與內容請求跟踪的某些差異組合。 |
| 機器人 | AEM 未預先識別和刪除的未知機器人可能會導致跟踪差異。 |
| 報表套裝 | 屬於同一 AEM 實例和域的頁面可能會將數據發送到不同的 Analytics 報表包。 |
| 第三方監控和安全工具 | 監控和安全掃描工具可能會為 AEM 生成未在 Analytics 報告中跟踪的內容請求。 |
| 預取請求 | 使用預取服務來預加載頁面以提高速度可能會導致內容請求流量顯著增加。 |
| DDOS | 儘管 Adobe 盡一切努力自動檢測和過濾來自 DDOS 攻擊的流量，但不能保證會檢測到所有可能的 DDOS 攻擊 |
| 流量攔截器 | 在瀏覽器中使用跟踪器阻止程序可能會選擇不跟踪某些請求。 |
| 防火牆 | 防火牆可能會阻止 Analytics 跟踪。這在企業防火牆中更為常見。 |

### 如果我想了解更多有關我的內容請求量的資訊呢? {#current-request-volumes}

如果您想進一步了解授權儀表板中顯示的內容請求量，您的 Adobe 團隊可以提供一份報告，顯示內容請求的主要數量驅動因素。請聯繫您的 Adobe 團隊或 Adobe 客戶服務，申請最高使用率報告。

### 如果我使用自己的 CDN 怎麼辦？ {#using-own-cdn}

授權儀表板只會顯示 Cloud Service CDN 追蹤的資料。如果您選擇使用自己的 CDN (BYOCDN)，您將按照合約中的規定每年向 Adobe 報告您的內容請求量。
