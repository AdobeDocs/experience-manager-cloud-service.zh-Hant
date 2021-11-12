---
title: 使用者存取新舊
description: 使用者存取新舊
source-git-commit: 82ec1283bfa8cc5ff48801521c291d438ff24122
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---


# 使用者存取新舊 {#user-access}

## 簡介 {#introduction}

Adobe高度重視應用程式的監控、可用性和效能。 為協助達成此目標，AEM as a Cloud Service提供存取自訂New Relic監控套裝的功能，作為標準產品產品的一部分，以確保您的團隊能最充分地掌握Adobe Experience ManagerCloud Service系統和環境效能量度。 本節說明在AEMas a Cloud Service環境上啟用的新舊物監控功能，以協助提升效能，並讓您充份運用AEMas a Cloud Service。

## AEMas a Cloud Service透過New Relic進行交易監控 — 價值主張 {#transaction-monitoring}

以下是New Relic Application Performance Monitoring for AEM as a Cloud Service的價值主張摘要：

* 直接存取專用的New Relic One帳戶(由Adobe支援管理的存取權)。

* 檢測的New Relic APM代理，用行號顯示精確的方法調用，包括外部依賴項和資料庫。

* 結合基礎架構層級監控和應用程式(Adobe Experience Manager)監控的關鍵量度，實現整體效能最佳化。

* 將AEMas a Cloud ServiceJMX Mbeans和運行狀況檢查直接暴露到新的Relic Insights度量中，以便對應用程式堆棧效能和運行狀況度量進行深入檢查。

## 存取AEMas a Cloud Service New Relic帳戶 {#accessing-new-relic}

您的專用New Relic帳戶將透過客戶服務參與由Adobe布建和管理。 Adobe仍為擁有者和管理員，並代表您布建帳戶，以提供您專用子帳戶的存取權。

若要存取與您的AEMas a Cloud Service計畫相關聯的New Relic子帳戶：

* 請訪問Admin Console中的「支援」頁簽以開啟請求。
* 請確定您的票證包含方案ID的詳細資訊，以及您要求Adobe團隊開啟New Relic存取權的使用者清單。
* 必須向所有用戶提供全名和有效的電子郵件地址。

   >[!NOTE]
   >請參閱 [AEMExperience Cloud支援入口網站](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) 以取得更多詳細資訊。

提供存取權後，New Relic會傳送確認電子郵件給每位使用者，讓使用者完成設定程式並登入。

如果使用者找不到原始帳戶確認電子郵件：

1. 導覽至New Relic的登入頁面，網址為 [login.newrelic.com/login](https://login.newrelic.com/login).

1. 選擇 **忘記密碼**.

   ![](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. 輸入帳戶電子郵件地址，然後選取 **傳送我的重設連結**.

   ![](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. 當New Relic的系統傳回電子郵件訊息時，請選取其中的連結，以再次確認您的帳戶。

   >[!NOTE]
   >如果您未收到New Relic寄來的電子郵件：
   >檢查 [垃圾郵件篩選器](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/). 若適用， [將New Relic新增至您的電子郵件允許清單](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
   >請提供支援票證的反饋，我們的團隊將幫助您進一步

1. 如果您完成註冊過程，並且由於電子郵件或密碼錯誤消息而無法登錄您的帳戶，請通過以下方式記錄支援票證： [Admin Console](https://adminconsole.adobe.com/).

### 驗證您的電子郵件 {#verify-email}

如果您在登入期間被要求驗證電子郵件，表示您的電子郵件已與多個帳戶關聯，且在登入期間將獲得驗證電子郵件的選項。 這可讓您選擇要存取的帳戶。 如果您未驗證電子郵件地址，New Relic會嘗試將您與您電子郵件地址相關聯的最近建立的使用者記錄登入。 若要避免在每次登入時驗證您的電子郵件，請按一下登入畫面中的「記住我」核取方塊。

如需更多協助，請透過 [AEM支援入口網站](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## 例外 {#exceptions}

AEM as a Cloud Service僅針對New Relic APM解決方案提供重點，不提供警報、記錄或API整合功能的支援。

如需AEMas a Cloud Service計畫New Relic產品的更多說明或其他指引，請透過 [AEM支援入口網站](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) 以求協助。

## 新Relic帳戶常見問題 {#faqs}

### Adobe會透過New Relic監視什麼？ {#adobe-monitor}

Adobe會透過New Relic APM Java外掛程式監控AEMas a Cloud Service製作、發佈和預覽（若有）服務。 Adobe可跨非生產和生產AEMas a Cloud Service環境啟用自訂New Relic APM遙測和監控。 您的New Relic帳戶已附加至一個主要Adobe維護帳戶，且有多個應用程式向其報告。

每個AEMas a Cloud Service環境各3個：

* 每個環境適用於製作服務的一個應用程式
* 每個環境（包括Golden Publish）適用於Publish服務的一個應用程式
* 針對每個環境預覽服務的一個應用程式
   >[!IMPORTANT]
   >每個應用程式都使用一個授權金鑰，AEMas a Cloud Service環境只會向一個New Relic帳戶報告。 New Relic APM和基礎架構的完整監控量度和事件都會保留7天。

### 誰可以存取New RelicCloud Service資料？ {#access-new-relic-cloud}

最多可授予團隊10名成員的完整讀取存取權。 讀取存取將包含New Relic代理程式收集的所有APM量度。

### 是否支援自訂SSO配置？ {#custom-sso}

由Adobe布建的New Relic帳戶目前不支援自訂SSO設定。

### 如果您已有內部新舊物品訂購，該怎麼辦？ {#new-relic-subscription}

名為New Relic One的New Relic全新可觀察性平台可讓Adobe支援群組和您的團隊在單一位置觀察、監控及檢視量度和事件。 New Relic One讓使用者能夠在有存取權的所有帳戶中進行搜尋，並以單一檢視將來自所有服務和主機的資料視覺化。 雖然Adobe支援團隊將使用New Relic和其他內部工具監控AEMas a Cloud Service應用程式，作為服務的一部分，但您的團隊仍可繼續利用New Relic進行內部托管服務和基礎架構。 他們將能夠直觀地顯示來自Adobe和客戶管理的New Relic帳戶的資料。

>[!NOTE]
>使用者必須擁有正確的權限，並且對兩個帳戶(Adobe和客戶管理的New Relic帳戶)使用相同的登入方法。


