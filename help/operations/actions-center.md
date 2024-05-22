---
title: 行動中心
description: 善用行動中心，方便處理事件和其他重要資訊
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: ddf94262c047ea0210b0759176f51d1220ac9c67
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 74%

---

# 行動中心 {#actions-center}

AEM as Cloud Service 在發生需要立即採取行動的嚴重事件時會傳送行動中心電子郵件，並提出主動建議以進行最佳化。例如，佇列阻塞或一組過期的憑證；您可在[下表](#supported-notification-types)檢視整套行動中心通知類型，通知類型會隨時間增加。

收到「作業中心」電子郵件通知時，您可以按一下該通知，開啟AEMas a Cloud Service的「作業中心」，並出現快顯視窗，顯示說明客戶應採取的作業的額外內容。

除了顯示有關剛剛按一下的電子郵件通知資訊外，行動中心還可充當中樞，讓您在其中查看和管理目前和較舊的通知組。<!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

有兩種基本通知類別會出現在行動中心：

1. 操作事件 - 事件已經發生，通常需要及時解決。例如，解析阻塞的佇列。
1. 主動建議 - Adobe 建議客戶應該在近期採取行動。例如，停止參考已棄用的 UI。

請參閱[下表](#supported-notification-types)了解行動忠目前支援的通知。

從行動中心，您可以選取特定的計畫和環境，這可對該範圍進行篩選。

## 設定 {#configuration}

若要配置接收行動中心的電子郵件通知，請建立[本文](/help/journey-onboarding/notification-profiles.md)所描述的產品設定檔，即「事件通知 - Cloud Service」和「主動通知 - Cloud Service」。還要指派貴組織的適當 Adobe ID 至這些設定檔。這可讓管理員確定哪些使用者有資格接收這些電子郵件通知。

>[!NOTE]
>行動中心電子郵件通知在組織層級執行，因此訂閱者將收到有關這些計畫中的所有計畫和環境通知。

## 詳細的使用者流程 {#detailed-user-flow}

按一下電子郵件即可進入「動作中心」，快顯視窗會顯示您所按通知的前後關聯，在某些情況下，還會顯示其他資訊的連結，說明如何採取更正動作。 您還可以直接存取行動中心：[https://experience.adobe.com/aem/actions-center](https://experience.adobe.com/aem/actions-center/)；您可以在行動中心選取相關的計畫和環境。

![事件詳細資料](/help/operations/assets/incident-details.png)

按一下&#x200B;**了解更多**&#x200B;連結可讓使用者導覽至本文，在該處參考下面[支援的通知類型表](#supported-notification-types) (提供採取何種動作的指引) 中的通知類型。

在行動通知中心，您可以看到其他最近通知的清單。建議您使用「動作」清單確認通知，以便向 Adobe 表明您的組織已了解該任務，並在稍後採取糾正措施後解決該通知。

![通知清單](/help/operations/assets/notification-list.png)

在大多數情況下，快顯視窗應該會提供所有解決問題所需的內容。 不過，如果Adobe支援有任何問題，您可以按一下 **聯絡支援人員** 快顯視窗中的連結。 這將彈出一個表格，您可以在表格中描述問題並提交它以建立支援票證，其中可包含對特定通知的參考，以便 Adobe 支援工程師了解相關內容。

![聯絡支援 1](/help/operations/assets/contact-support1.png)

![聯絡支援 2](/help/operations/assets/contact-support2.png)

與所有支援票證一樣，它會出現在 [Adobe Admin Console 的「支援案例」標籤](https://helpx.adobe.com/tw/enterprise/using/support-for-enterprise.html)中，您可以在其中追蹤它並新增其他評論。

![Admin Console 支援](/help/operations/assets/admin-console-support.png)

## 哪些通知會出現？ {#which-notification}

AEM as a Cloud Service 有多種類型的通知，但只有一部分出現在行動通知中心，如下表所示。

| 通知類型 | 說明 | 如何設定 | 出現在行動中心 |
|---|---|---|---|
| 操作事件 | 需要立即採取行動的嚴重事件 | 指派給「事件通知 - Cloud Service」產品設定檔的使用者 | X |
| 主動建議 | 應該計畫的最佳化 | 指派給「主動通知 - Cloud Service」產品設定檔的使用者 | X |
| Cloud Manager 管道狀態 | 有關管道狀態的資訊 | 使用者具有企業所有者、方案管理員或部署管理員角色，已選取「其他」核取方塊 [Experience Cloud偏好設定](https://experience.adobe.com/preferences)， as [此處說明](/help/implementing/cloud-manager/notifications.md). |   |

## 支援的通知類型 {#supported-notification-types}

下表列有行動中心目前支援的通知類型。目前僅限於生產環境可使用通知。

| 通知類型 | 相關產品簡介 | 糾正措施 |
|---------------------------------|-------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 鎖定的複製佇列 | 事件 | 按照[複製文件](/help/operations/replication.md#troubleshooting)中的說明解鎖佇列 |
| 無效的GraphQL查詢 | 事件 | 參考「 」以修正無效的GraphQL查詢 [持續的GraphQL查詢疑難排解檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/headless/graphql-api/persisted-queries-troubleshoot.html) |
| 即將到期的 S2S 認證 | 主動 | 在[為伺服器端 API 產生權杖文件](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials)中，了解如何重新整理認證 |
| 來源處的流量尖峰 | 事件 | 透過設定在低於來源預設流量尖峰警報的臨界值處觸發的速率限制流量篩選規則，Protect您的來源。  請參閱 [使用流量規則封鎖DoS和DDoS攻擊](/help/security/traffic-filter-rules-including-waf.md#blocking-dos-and-ddos-attacks-using-traffic-filter-rules) 流量篩選規則檔案的區段，其中會參考教學課程。 |
