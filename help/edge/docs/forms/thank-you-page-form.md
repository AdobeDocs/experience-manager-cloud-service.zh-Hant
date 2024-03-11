---
title: 提交後設定感謝頁面或重新導向表單
description: 了解如何設定 Forms 區塊的感謝頁面和重新導向，以最佳化使用者體驗並簡化使用者歷程。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: e6c66b22-dc52-49e3-a920-059adb5be22f
source-git-commit: 4144f9704aaf17ea684be147395adc3aa31641f2
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 80%

---

# 提交後顯示感謝頁面或重新導向表單

在使用者提交表單後，透過感謝頁面或重新導向提供無縫體驗至關重要。這些元素不僅可以向使用者確認成功提交，還可以提高使用者滿意度並引導他們進行更深入的歷程。

* **感謝頁面**：感謝頁面是使用者體驗的重要基礎，一方面可加強品牌本身識別度，另一方面可提供保證並傳達重要訊息。此頁面是對使用者行為的直接認可，讓他們產生一種完成後的滿足感。

* **重新導向**：重新導向可發揮關鍵作用，旨在引導使用者前往相關目的地、提高最佳參與度且最後達到更高轉換率。重新導向可無縫引導使用者進入下一步歷程，確保使用者得到流暢的導覽體驗。例如，在收集原始的詳細資訊後，系統會將使用者重新導向付款頁面。

在最適化Forms區塊中，預設行為是顯示感謝頁面。 但是，您可以靈活地自訂這項體驗，以滿足您的特定需求。選項包括：    

* [設定感謝頁面和訊息以達到您的品牌和溝通目標](#configuring-the-thank-you-page-and-message)
* [提交後將使用者重新導向至另一個頁面，以便使用者採取進一步動作](#redirect-users-to-another-page-post-submission)

## 設定感謝頁面和訊息

最適化Forms區塊的預設行為是在提交時顯示「感謝您」頁面。 請依照下列步驟，為您的最適化Forms區塊設定「感謝您」頁面：

1. 在 Microsoft SharePoint 或 Google Workspace 上，存取 AEM Edge Delivery 專案資料夾。
1. 在專案目錄內，建立一個名為「感謝」的 Microsoft Word 或 Google Docs 檔案。
1. 將您的感謝訊息新增至「感謝」檔案中。 </br>

   ![感謝頁面範例](/help/edge/assets/sample-thankyou-page.png)

1. 使用 AEM Sidekick 預覽和發佈「感謝」檔案。

您的最適化Forms區塊會在表單提交時顯示「感謝您」頁面。

## 提交後將使用者重新導向至另一個頁面

依預設，最適化Forms區塊會將使用者重新導向至「感謝您」頁面。 若要將使用者重新導向至其他頁面，而非預設的「感謝」頁面，您有兩個選項：

* [將「感謝」頁面更換為其他頁面](#replace-the-existing-thankyou-page)
* [使用網站重新導向功能，進行「感謝」頁面的重新導向](#use-website-redirects-for-thankyou-page-redirection)

### 取代「感謝」頁面

1. 開啟 &quot;[EDS Project]/blocks/form/form.js&quot; 檔案進行編輯。
1. 將下行中的 `thankyou` 頁面變更為您選擇的頁面：

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   例如，

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'payment';
   ```

   >[!NOTE]
   >
   > 在Microsoft SharePoint或Google Workspace上，確認Edge Delivery Services專案資料夾中存在相同名稱的頁面。 如果該頁面不存在，請繼續建立並發佈。

1. 繼續將更新的「form.js」資料夾及其基礎檔案簽入GitHub上的Edge Delivery Services專案。 此更新可確保表單現在會重新導向至指定的更新頁面。

1. 確保該頁面存在於您的 EDS 專案資料夾中並將其發布。


### 使用網站重新導向功能，進行「感謝」頁面的重新導向

提交表單後將使用者重新導向至另一個頁面，可提供相關資訊、確認動作並引導使用者前往期望的結果頁面，藉此加強使用者體驗。例如，

* 使用者填寫購買表單後，他們將被重新導向至付款頁面，以安全方式完成交易。
* 提交活動或網路研討會的註冊表單後，使用者將被重新導向至顯示活動詳細資訊 (例如日期、時間和地點) 的確認頁面。

若要將「感謝」頁面重新導向至其他頁面，請使用「[網站重新導向](https://www.aem.live/docs/redirects)」試算表。


## 另請參閱

{{see-more-forms-eds}}