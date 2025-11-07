---
title: 行動中心
description: 善用行動中心，方便處理事件和其他重要資訊
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
feature: Operations
role: Admin
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 48%

---

# 行動中心 {#actions-center}

AEM as Cloud Service 在發生需要立即採取行動的嚴重事件時會傳送行動中心電子郵件，並提出主動建議以進行最佳化。例如，佇列阻塞或一組過期的憑證；您可在[下表](#supported-notification-types)檢視整套行動中心通知類型，通知類型會隨時間增加。

收到「動作中心」電子郵件通知時，可以按一下該通知以開啟AEM as a Cloud Service的「動作中心」，並出現快顯視窗，顯示說明客戶應採取的動作的其他內容。

除了顯示有關剛剛按一下的電子郵件通知資訊外，行動中心還可充當中樞，讓您在其中查看和管理目前和較舊的通知組。<!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

有兩種基本通知類別會出現在行動中心：

1. 操作事件 - 事件已經發生，通常需要及時解決。例如，解析阻塞的佇列。
1. 主動建議 - Adobe 建議客戶應該在近期採取行動。例如，停止參考已棄用的 UI。

請參閱[下表](#supported-notification-types)了解行動忠目前支援的通知。

從行動中心，您可以選取特定的計畫和環境，這可對該範圍進行篩選。

## 設定 {#configuration}

若要設定接收動作中心電子郵件通知，請依照[通知設定檔](/help/journey-onboarding/notification-profiles.md)下所述建立產品設定檔，即事件通知 — Cloud Service和主動通知 — Cloud Service。 還要指派貴組織的適當 Adobe ID 至這些設定檔。這可讓管理員確定哪些使用者有資格接收這些電子郵件通知。

>[!NOTE]
>行動中心電子郵件通知在組織層級執行，因此訂閱者將收到有關這些計畫中的所有計畫和環境通知。

## 詳細的使用者流程 {#detailed-user-flow}

按一下電子郵件即可進入「動作中心」，快顯視窗會顯示您所按通知的前後關聯，在某些情況下，還會顯示其他資訊的連結，說明如何採取更正動作。 您還可以直接存取行動中心：[https://experience.adobe.com/aem/actions-center](https://experience.adobe.com/aem/actions-center/)；您可以在行動中心選取相關的計畫和環境。

![事件詳細資料](/help/operations/assets/incident-details.png)

按一下&#x200B;**了解更多**&#x200B;連結可讓使用者導覽至本文，在該處參考下面[支援的通知類型表](#supported-notification-types) (提供採取何種動作的指引) 中的通知類型。

在行動通知中心，您可以看到其他最近通知的清單。建議您使用「動作」清單確認通知，以便向 Adobe 表明您的組織已了解該任務，並在稍後採取糾正措施後解決該通知。

![通知清單](/help/operations/assets/notification-list.png)

在大多數情況下，快顯視窗應該會提供所有解決問題所需的內容。 不過，如果Adobe支援有任何問題，您可以按一下快顯視窗中的&#x200B;**聯絡支援**&#x200B;連結。 這將彈出一個表格，您可以在表格中描述問題並提交它以建立支援票證，其中可包含對特定通知的參考，以便 Adobe 支援工程師了解相關內容。

![聯絡支援 1](/help/operations/assets/contact-support1.png)

![聯絡支援 2](/help/operations/assets/contact-support2.png)

與所有支援票證一樣，它會出現在 [Adobe Admin Console 的「支援案例」標籤](https://helpx.adobe.com/tw/enterprise/using/support-for-enterprise.html)中，您可以在其中追蹤它並新增其他評論。

![Admin Console 支援](/help/operations/assets/admin-console-support.png)

## 哪些通知會出現？ {#which-notification}

AEM as a Cloud Service 有多種類型的通知，但只有一部分出現在行動通知中心，如下表所示。

| 通知類型 | 說明 | 如何設定 | 出現在行動中心 |
|---------------------------------|-----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| 操作事件 | 需要立即採取行動的嚴重事件 | 指派給「事件通知 - Cloud Service」產品設定檔的使用者 | X |
| 主動建議 | 應該計畫的最佳化 | 指派給「主動通知 - Cloud Service」產品設定檔的使用者 | X |
| Cloud Manager 管道狀態 | 有關管道狀態的資訊 | 在[Experience Cloud偏好設定](https://experience.adobe.com/preferences)中選取「其他」核取方塊的使用者（具有企業所有者、方案管理員或部署管理員角色），請參閱[通知](/help/implementing/cloud-manager/notifications.md)。 |                           |

## 支援的通知類型 {#supported-notification-types}

下表列有行動中心目前支援的通知類型。目前僅限於生產環境可使用通知。

| 通知類型 | 相關產品簡介 | 糾正措施 |
|---------------------------------|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 鎖定的複製佇列 | 事件 | 按照[複製文件](/help/operations/replication.md#troubleshooting)中的說明解鎖佇列 |
| 無效的GraphQL查詢 | 事件 | 參考[持續的GraphQL查詢疑難排解檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/headless/graphql-api/persisted-queries-troubleshoot.html?lang=zh-Hant)，修正無效的GraphQL查詢 |
| 來源處的流量尖峰 | 事件 | 設定在低於來源預設流量尖峰警報觸發的速率限制流量篩選規則，以保護您的來源。  請參閱參考教學課程之流量篩選規則檔案中的[使用流量規則封鎖DoS和DDoS攻擊](/help/security/traffic-filter-rules-including-waf.md#blocking-dos-and-ddos-attacks-using-traffic-filter-rules)一節。 |
| 已觸發CDN流量篩選器規則 | 事件 | 如果相符的流量篩選規則反映攻擊，而您的網站沒有封鎖該流量，請在封鎖模式中設定流量篩選規則來保護您的網站。 請參閱流量篩選規則檔案中的[使用流量篩選規則(包括WAF規則)保護網站](/help/security/traffic-filter-rules-including-waf.md#tutorial-protecting-websites)一節，其中會參考教學課程。 |
| Splunk記錄轉送錯誤 | 事件 | 檢查您的Splunk端點是否正常運作，以及是否可以從您的AEM Cloud Service環境連線。 如需記錄轉送的詳細資訊，請瀏覽[Splunk記錄轉送檔案](/help/implementing/developing/introduction/logging.md#splunk-logs)。 如果您需要協助疑難排解，或需要變更記錄設定，請向Adobe提出支援票證。 |
| 頁面包含大量節點 | 主動 | 減少頁面中的節點總數。 請參閱[頁面複雜性檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-pattern-detection/table-of-contents/pcx) |
| 大量執行中的工作流程例項 | 主動 | 終止不再需要的執行中工作流程。 瞭解如何[設定清除工作](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/operations/maintenance) |
| 即將到期的 S2S 認證 | 主動 | 在[為伺服器端 API 產生權杖文件](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)中，了解如何重新整理認證 |
| 高連線計數 | 主動 | 瞭解在[連線集區以及進階網路檔案](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking)中的連線集區 |
| 已棄用的服務使用者對應 | 主動 | 瞭解如何使用較新的Sling服務使用者對應格式，如[Sling服務使用者對應和服務使用者定義的最佳實務](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/security/best-practices-for-sling-service-user-mapping-and-service-user-definition)中所述 |
| 高連線計數 | 主動 | 在[進階網路檔案](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking)中瞭解連線集區 |
| 直接新增到自訂群組的使用者 | 主動 | 使用者需要新增到相關的IMS群組，這些IMS群組需要新增為AEM群組的成員。 符合[IMS最佳實務](/help/security/ims-support.md) |
| 缺少JCR內容 | 主動 | 新增遺失的JCR內容節點。 請參閱[Assets內容驗證器檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-pattern-detection/table-of-contents/acv) |
| 已完成的工作流程未清除 | 主動 | 將工作流程例項的數目降至最低，並透過清除超過90天之前的工作流程例項來改善效能。 瞭解如何[設定維護工作](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/operations/maintenance) |
| 頁面中缺少Sling資源型別 | 主動 | 新增缺少的Sling資源型別節點。 請參閱[Assets內容驗證器檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-pattern-detection/table-of-contents/acv) |
| 緩慢查詢 | 主動 | 依照[JCQ查詢速查表](https://experienceleague.adobe.com/docs/experience-manager-65/assets/JCR_query_cheatsheet-v1.1.pdf?lang=zh-Hant)的建議，定義正確的索引定義，以修正緩慢查詢 |
| 沒有索引的查詢 | 主動 | 避免執行未使用索引的查詢 — [索引檔案的連結](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/operations/indexing) |
| 已棄用的資料庫警報 | 主動 | 將已棄用的套件取代為其建議的較新版本（如[棄用文章](/help/release-notes/deprecated-removed-features.md)中所述），以保持應用程式的安全性和效能 |
| 已棄用的設定警示 | 主動 | 將已棄用的設定取代為其建議的較新版本（如[Deprecation article](/help/release-notes/deprecated-removed-features.md)中所述），以保持應用程式的安全性和效能 |
