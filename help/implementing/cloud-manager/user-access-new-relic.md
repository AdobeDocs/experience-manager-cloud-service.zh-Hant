---
title: 新舊一號
description: 瞭解針對as a Cloud Service的New Relic One應用程式效能監控(APM)服務AEM以及您如何訪問該服務。
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 09049213eaf92830dc0e0d4c0885017c69a5d56e
workflow-type: tm+mt
source-wordcount: '1622'
ht-degree: 1%

---


# 新舊一號 {#user-access}

瞭解針對as a Cloud Service的New Relic One應用程式效能監控(APM)服務AEM以及您如何訪問該服務。

## 簡介 {#introduction}

Adobe非常重視應用程式的監控、可用性和效能。 AEM New Relic One監控套件是標準產品的一部分，可讓您的團隊最大限度地瞭解您的AEMas a Cloud Service系統和環境效能指標。

本文檔介紹如何管理對New Relic One應用程式效能監控(APM)功能的訪問，這些功能在您的AEMas a Cloud Service環境中啟用，有助於支援效能，並使您能夠最大限度地利用AEMas a Cloud Service。

建立新生產程式後，將自動建立與您的AEMas a Cloud Service程式關聯的New Relic One子帳戶。

## 功能 {#transaction-monitoring}

New Relic One APM for AEM as a Cloud Service有許多功能。

* 直接訪問專用的New Relic One帳戶(由Adobe支援管理的訪問)

* 已檢測的New Relic One APM代理，它顯示具有行號（包括外部依賴關係和資料庫）的精確方法調用

* 通過將基礎架構級監控和應用程式(Adobe Experience Manager)監控的關鍵指標結合起來，實現整體效能優化

* 直接在AEMNew Relic Insights指標中暴露as a Cloud Service的JMX Mbean和運行狀況檢查，從而能夠深入檢查應用程式堆棧效能和運行狀況指標。

## 管理New Relic One用戶 {#manage-users}

按照以下步驟定義與您的as a Cloud Service程式關聯的New Relic One子帳戶的AEM用戶。

>[!NOTE]
>
>中的用戶 **業務所有者** 或 **部署管理器** 必須登錄角色才能管理New Relic One用戶。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織。

1. 按一下要為其管理New Relic One用戶的程式。

1. 切換到 **環境** 從 **計畫概述** 的 **環境** 按鈕。

1. 在 **環境** 螢幕中，按一下螢幕頂部旁邊的省略號按鈕 **添加環境** 按鈕

1. 在省略號菜單中，按一下 **管理用戶**。

   ![管理用戶](assets/newrelic-manage-users.png)

1. 在 **管理New Relic用戶** 對話框，輸入要添加的用戶的姓和名，然後按一下 **添加** 按鈕 對要添加的所有用戶重複此步驟。

   ![添加用戶](assets/newrelic-add-users.png)

1. 要刪除New Relic One用戶，請按一下表示用戶的行右端的刪除按鈕。

1. 按一下 **保存** 建立用戶。

定義用戶後，New Relic會向您授予訪問權限的每個用戶發送確認電子郵件，以便用戶完成設定過程並登錄。

>[!NOTE]
>
>如果要管理New Relic One用戶，您還必須將自己添加為用戶，以便也具有訪問權限。 是 **業務所有者** 或 **部署管理器** 不足以訪問New Relic One。 您還必須將自己建立為用戶。

## 激活新舊物單用戶帳戶 {#activate-account}

建立New Relic One用戶帳戶後，如預覽部分所述 [管理New Relic One用戶](#manage-users),New Relic向這些用戶發送確認電子郵件至提供的地址。 要使用這些帳戶，用戶必須首先通過重置其密碼來激活其使用New Relic的帳戶。

按照以下步驟以New Relic用戶身份激活帳戶。

1. 按一下New Relic電子郵件中提供的連結。 這將開啟瀏覽器到「新建檔案」登錄頁。

1. 在「新建」登錄頁上，選擇 **忘記密碼了？**。

   ![新建Relic登錄](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. 輸入您收到確認電子郵件的電子郵件地址，然後選擇 **發送我的重置連結**。

   ![輸入電子郵件地址](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic將向您發送一封包含確認帳戶連結的電子郵件。

如果您未收到New Relic的確認電子郵件，請參閱 [疑難解答部分。](#troubshooting)

## 訪問新舊檔案一 {#accessing-new-relic}

一旦你 [已激活新舊物帳戶，](#activate-account) 您可以通過雲管理器或直接訪問New Relic One。

要通過雲管理器訪問New Relic One:

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織。

1. 按一下要訪問New Relic One的程式。

1. 切換到 **環境** 從 **計畫概述** 的 **環境** 按鈕。

1. 在 **環境** 螢幕中，按一下螢幕頂部旁邊的省略號按鈕 **添加環境** 按鈕

1. 在省略號菜單中，按一下 **開啟新舊檔案**。

1. 在開啟的新瀏覽器頁籤中，登錄到New Relic One。

要直接訪問New Relic One:

1. 導航到New Relic的登錄頁，位於 [`https://login.newrelic.com/login`](https://login.newrelic.com/login)

1. 登錄新舊一號。

### 驗證您的電子郵件 {#verify-email}

如果在登錄New Relic One時要求您驗證電子郵件，這意味著您的電子郵件與多個帳戶相關聯。 這允許您選擇要訪問的帳戶。

如果您未驗證您的電子郵件地址，New Relic將嘗試使用與您的電子郵件地址關聯的最近建立的用戶記錄登錄。 要避免在每次登錄過程中驗證您的電子郵件，請按一下 **記住我** 複選框。

要獲得更多幫助，請通過 [支AEM持門戶](https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html)。

## New Relic One訪問故障排除 {#troubleshooting}

如果您被添加為New Relic One用戶，如一節中所述 [管理New Relic One用戶](#manage-users) 無法找到原始帳戶確認電子郵件，請執行以下步驟。

1. 導航到New Relic的登錄頁，位於 [`login.newrelic.com/login`](https://login.newrelic.com/login)。

1. 選擇 **忘記密碼了？**。

   ![新建Relic登錄](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. 輸入用於建立帳戶的電子郵件地址，然後選擇 **發送我的重置連結**。

   ![輸入電子郵件地址](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic將向您發送一封包含確認帳戶連結的電子郵件。

如果您完成註冊過程並且由於電子郵件或密碼錯誤消息而無法登錄帳戶，請通過以下方式記錄支援票證： [Admin Console。](https://adminconsole.adobe.com/)

如果您未收到New Relic發來的電子郵件：

* 檢查 [垃圾郵件過濾器](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/)。
* 如果適用， [將新舊內容添加到電子郵件允許清單](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist)。
* 如果這兩個建議都不有幫助，請提供有關支援票證的反饋，Adobe支援團隊將進一步幫助您。

## 限制 {#limitations}

將用戶添加到New Relic One時適用以下限制：

* 最多可以添加25個用戶。 如果已達到最大用戶數，請刪除用戶以便能夠添加新用戶。
* 添加到New Relic的用戶類型為 **受限** 參考 [New Relic文檔以獲取詳細資訊。](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/#:~:text=In%20general%2C%20Admins%20take%20responsibility,Restricted%20Users%20can%20use%20them.&amp;text=1%20或%20多%20個人%20who，更改)%20any%20新%20Relic%20功能。)
* AEMas a Cloud Service僅提供New Relic One APM解決方案，不支援警報、日誌記錄或API整合。

有關您的as a Cloud Service計畫的New Relic One產品的更多幫助或其AEM他指導，請通過 [支AEM持門戶](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html)。

## 關於新羅利克一號的常見問題 {#faqs}

### Adobe用New Relic One監控什麼？ {#adobe-monitor}

Adobe通AEM過New Relic One的Java插件監控as a Cloud Service作者、發佈和預覽（如果可用）服務。 Adobe支援跨非生產和生產as a Cloud Service環境的定製New Relic One APM遙測AEM和監視。

您的New Relic One帳戶附加到一個主Adobe維護帳戶，並有多個應用程式報告到該帳戶：每個as a Cloud ServiceAEM環境3個。

* 每個環境為作者服務提供一個應用程式
* 每個環境的發佈服務（包括Golden Publish）的一個應用程式
* 每個環境的預覽服務一個應用程式

請注意:

* 每個應用程式使用一個許可證密鑰。
* AEMas a Cloud Service環境僅報告一個New Relic One帳戶。
* New Relic One的完整監控指標和事件將保留七天。

### 誰可以訪問New Relic One雲服務資料？ {#access-new-relic-cloud}

您的團隊最多10個成員將獲得完全讀取權限。 讀取訪問將包括由New Relic One代理收集的所有APM度量。

### 是否支援自定義SSO配置？ {#custom-sso}

由Adobe設定的New Relic One帳戶不支援自定義SSO配置。

### 如果我已經擁有內部New Relic訂閱，該怎麼辦？ {#new-relic-subscription}

New Relic One是New Relic的新可觀測平台，它使Adobe支援和您的團隊能夠在一個位置觀察、監控和查看度量和事件。

New Relic One使用戶能夠搜索其有權訪問的所有帳戶，並在一個視圖中顯示來自所有服務和主機的資料。

Adobe支援將使用New Relic AEM One和其他內部工具監控as a Cloud Service應用程式，作為服務的一部分，您的團隊可以繼續利用New Relic進行內部托管服務和基礎架構。 他們將能夠可視化AdobeNew Relic One帳戶和客戶管理的New Relic帳戶的資料。

>[!NOTE]
>
>要在New Relic One中查看兩個資料集，用戶必須具有權限，並且對兩個帳戶(AdobeNew Relic One和客戶管理的New Relic帳戶)使用相同的登錄方法。
