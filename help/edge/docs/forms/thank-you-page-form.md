---
title: 設定 EDS Forms 的感謝頁面
description: 瞭解如何為EDS Forms設定感謝頁面和重新導向，以最佳化使用者體驗並簡化使用者歷程。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: cadeccd916884ca2437e2b2684771c181cc8281e
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 7%

---


# 提交後顯示感謝頁面或重新導向表單

使用者提交表單後，透過感謝頁面或重新導向來提供順暢的體驗至關重要。 這些元素不僅可確認提交成功，也可提升使用者滿意度，並指引他們更進一步歷程。

* **感謝頁面**：感謝頁面是使用者體驗的基石，可在強化品牌身分的同時，提供安慰和傳達重要資訊。 它可直接承認使用者的行為，培養完成感和滿意感。

* **重新導向**：重新導向在引導使用者前往相關目的地、最佳化參與以及最終提高轉換率方面，扮演著關鍵角色。 重新導向可順暢地引導使用者踏上歷程的下一步，確保順暢的導覽體驗。 例如，在收集初始詳細資料後，將使用者重新導向至付款頁面。

在最適化Forms區塊中，預設行為是顯示感謝頁面。 不過，您還是可以靈活地量身打造此體驗，以符合您的特定需求。 選項包括：

* [設定感謝頁面和訊息，以符合您的品牌和溝通目標](#configuring-the-thank-you-page-and-message)
* [提交後重新導向使用者至其他頁面](#redirect-users-to-another-page-post-submission)，進一步增強其歷程

## 設定感謝頁面和訊息

最適化Forms區塊的預設行為是在提交時顯示「感謝您」頁面。 請依照下列步驟，為您的最適化Forms區塊設定「感謝您」頁面：

1. 在Microsoft SharePoint或Google Workspace上存取AEM Edge Delivery專案資料夾。
1. 在您的專案目錄中建立名為「感謝您」的Microsoft Word或Google Docs檔案。
1. 將您的感謝訊息新增至「感謝您」檔案。 </br>

   ![感謝頁面範例](/help/edge/assets/sample-thankyou-page.png)

1. 使用AEM Sidekick來預覽和發佈「感謝您」檔案。

您的最適化Forms區塊會在表單提交時顯示「感謝您」頁面。

## 將使用者重新導向至提交後的另一個頁面

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

## 了解更多

* [表單元件](/help/edge/docs/forms/form-components.md)
* [表單欄位屬性](/help/edge/docs/forms/eds-form-field-properties)
* [建立並預覽表單](/help/edge/docs/forms/create-forms.md)
* [啟用表單來傳送資料](/help/edge/docs/forms/submit-forms.md)
* [將表單發佈到網站頁面](/help/edge/docs/forms/publish-eds-forms.md)
* [新增驗證至表單欄位](/help/edge/docs/forms/validate-forms.md)
* [改變主題和樣式風格](/help/edge/docs/forms/style-theme-forms.md)
