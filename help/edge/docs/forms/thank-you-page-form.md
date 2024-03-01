---
title: 設定 EDS Forms 的感謝頁面
description: 瞭解如何為EDS Forms設定感謝頁面和重新導向，以最佳化使用者體驗並簡化使用者歷程。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: e2970c7a141025222c6b119787142e7c39d453af
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 2%

---


# 在最適化Forms區塊中設定感謝頁面和重新導向

感謝您的頁面和重新導向，是增強使用者體驗的重要方面，可為使用者提供確認、清楚的溝通，以及表單提交後的順暢導覽。

## 設定感謝頁面

感謝頁面可讓使用者安心，讓組織傳達重要資訊，同時強化品牌識別。 請依照下列步驟，為EDS Forms設定感謝頁面：

1. 在Microsoft SharePoint或Google Workspace上存取AEM Edge Delivery專案資料夾。
1. 在您的專案目錄中建立名為「感謝您」的Microsoft Word或Google Docs檔案。
1. 將您的感謝訊息新增至「感謝您」檔案。
   ![感謝頁面範例](/help/edge/assets/sample-thankyou-page.png)
1. 利用AEM Sidekick來預覽和發佈「感謝您」檔案。

## 提交後重新導向使用者

重新導向透過將使用者引導到相關目的地、最佳化參與以及提高轉換率，促進無縫的使用者歷程。

依預設，最適化Forms區塊會將使用者重新導向至「感謝您」頁面。 若要將使用者重新導向至預設「感謝您」頁面以外的頁面，您有兩個選項：

* 請以其他頁面取代現有的「感謝您」頁面，或
* 將「感謝您」頁面重新導向至您選擇的另一個頁面。

### 取代現有的「感謝您」頁面

1. 開啟&quot;[EDS專案]/blocks/form/form.js」檔案進行編輯。
1. 變更 `thankyou` 下一行中的頁面放入您選擇的頁面：

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   例如，

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'payment';
   ```

   >[!NOTE]
   >
   > 在Microsoft SharePoint或Google Workspace上，確定您的Edge Delivery Service專案資料夾中存在同名頁面。 如果頁面不存在，請繼續建立並發佈。

1. 繼續將更新的「form.js」資料夾及其基礎檔案簽入GitHub上的Edge Delivery Service專案。 此更新可確保表單現在會依指定重新導向至更新的頁面。

1. 確定頁面存在於您的EDS專案資料夾中並加以發佈。


### 使用網站重新導向

設定網站重新導向，將「感謝您」頁面導向其他頁面。 請參閱 [重新導向檔案](https://www.aem.live/docs/redirects) 以取得詳細指示。


