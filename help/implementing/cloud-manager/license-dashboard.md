---
title: 授權儀表板
description: Cloud Manager提供控制面板，供您輕鬆檢視組織或租用戶可用的AEMaaCS產品權益。
exl-id: bf0f54a9-fe86-4bfb-9fa6-03cf0fd5f404
source-git-commit: b5078c849c9fa088546f5df1fcbef1dec59f3cdb
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 2%

---

# 授權儀表板 {#license-dashboard}

Cloud Manager提供控制面板，供您輕鬆檢視組織或租用戶可用的AEMaaCS產品權益。

## 總覽 {#overview}

Cloud Manager授權控制面板可讓您輕鬆存取下列資訊：

1. 您在所有計畫中都可獲得的解決方案權利，包括使用的內容和可用的內容
1. Sites解決方案內容要求耗用量度（依月份趨勢）

## 使用授權控制面板 {#using-dashboard}

若要存取您的授權控制面板，請依照下列步驟操作。

>[!NOTE]
>
>中的使用者 **業務負責人** 角色必須登入才能檢視授權控制面板。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織。

1. 在產品概觀頁面上，切換至 **授權** 標籤。

![授權儀表板](assets/license-dashboard.png)

控制面板分為三個區段，顯示您：

* **解決方案**  — 本節概述您已授權的解決方案，例如Sites或Assets。
* **附加元件**  — 本節概括了您可用的授權解決方案的哪些附加元件。
* **沙箱與開發環境**  — 本節概述您可用的環境。

每個區段都會總結可用項目以及目前的使用方式（如果有的話）。 目前，即使租用戶中存在其他解決方案，也只會顯示Sites解決方案。

* 此 **狀態** 欄會顯示未使用與租用戶可用的權益總數。
* 此 **在上配置** 欄指示已應用解決方案權利的程式。
   * 只有在已建立生產環境或已存在生產環境（如果已在其上執行更新管道）時，才會將權限視為使用。
* 此 **使用狀況** 欄會在按一下後，以圖表形式顯示過去12個月中使用的內容請求。

>[!TIP]
>
>請參閱 [Admin Console概述](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 了解如何透過Admin Console管理整個組織的Adobe權益。

## 常見問答 {#faq}

### 什麼是內容要求？ {#what-is-a-content-request}

內容要求是進入AEM Sites或任何客戶提供的快取系統（例如內容傳送網路）的要求，以HTML格式（以頁面檢視）或JSON格式（以API呼叫）傳送內容或資料。

在第一快取系統的入口處測量每個頁面檢視或每五個API呼叫會計算一個內容要求，以接收內容要求。 內容要求只會計入生產環境。

內容請求會排除由Adobe或代表促銷者為提供產品和服務而起始的請求或活動。 Adobe識別的使用者代理流量也會排除來自機器人程式、編目程式，以及與常見搜尋引擎和社交媒體服務相關的編目程式。

### Adobe Experience Manager如何測量內容要求？ {#how-are-content-requests-measured}

內容要求會在AEM as a Cloud Service的邊緣伺服器上追蹤。 來源流量不會計入內容要求。 AEMas a Cloud Service內建的CDN會追蹤有效的HTML和JSON要求。

AEM也有排除知名機器人的規則，包括定期造訪網站的知名服務，以重新整理其搜尋索引或服務。

### 我的AEM報表為何顯示與Analytics內容請求不同的結果？ {#why-are-reports-different}

如下表所匯總，內容要求與組織的Analytics報表工具會有差異。

| 差異原因 | 說明 |
|---|---|
| 標記 | 所有以AEM內容請求來追蹤的頁面，都可能或不會以Analytics追蹤來標籤。 所有以AEM內容請求追蹤的API呼叫，都不會被組織的Analytics工具加上標籤。<br>頁面或API呼叫可經過標籤，以追蹤動作或僅經過不重複頁面檢視，而非所有檢視。 |
| Tag Management規則 | 標籤管理規則設定可能會導致頁面上出現各種資料收集設定，導致內容要求追蹤不一致的部分結合。 |
| 機器人 | 未預先識別且由AEM移除的未知機器人可能會造成追蹤差異。 |
| 報表套裝 | 屬於相同AEM例項和網域的頁面可能會傳送資料至不同的Analytics報表套裝。 |
| 協力廠商監控與安全性工具 | 監控和安全性掃描工具可能會為AEM產生未在Analytics報表中追蹤的內容要求。 |
| 預先擷取請求 | 使用預先擷取服務來預先載入頁面以提升速度，可能會導致內容要求流量大幅增加。 |
| DDOS | 雖然Adobe盡了一切努力來自動檢測和過濾來自DDOS攻擊的流量，但不能保證所有可能的DDOS攻擊都會被檢測到 |
| 流量封鎖程式 | 在瀏覽器中使用追蹤器封鎖程式可能會選擇退出某些請求不予追蹤。 |
| 防火牆 | 防火牆可能會封鎖Analytics追蹤。 這在公司防火牆中更常見。 |

### 如果我想要進一步了解我的內容要求卷，該怎麼辦？ {#current-request-volumes}

如果您想要進一步深入分析「授權控制面板」中顯示的內容要求量，您的Adobe團隊可提供報表，以顯示內容要求的最大數量驅動因素。 請洽詢您的Adobe團隊或Adobe客戶服務，以要求最常使用量報表。

### 如果我使用自己的CDN呢？ {#using-own-cdn}

「授權控制面板」只會顯示Cloud ServiceCDN追蹤的資料。  如果您選擇自攜CDN(BYOCDN)，則會依照合約中的說明，每年向Adobe回報內容要求量。
