---
title: 建立網站
description: 瞭解如何使用AEM建立網站，並使用網站範本定義網站的樣式和結構。
feature: Administering
role: Admin
exl-id: 9c71c167-2934-4210-abd9-ab085b36593b
solution: Experience Manager Sites
source-git-commit: 34c2604c7dcc2a1b27f617fe2d88eeb7496b3456
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 27%

---

# 建立網站 {#creating-site}

{{traditional-aem}}

瞭解如何使用AEM建立網站，並使用網站範本定義網站的樣式和結構。

## 概觀 {#overview}

必須先建立網站，內容作者才能建立含有內容的頁面。 這通常會由定義網站初始結構的AEM管理員執行。 使用網站範本可讓您快速且靈活地建立網站。

AEM快速網站建立工具可讓非開發人員使用網站範本，從頭開始快速建立網站。

建立後，快速建立網站工具還可讓您快速為 AEM 網站自訂主題並建立風格 (JavaScript、CSS 和靜態資源)。這使得前端開發人員即使不懂 AEM 也能與內容建立者分開且並行工作。AEM 管理員只需下載網站主題並將其提供給前端開發人員，前端開發人員使用他們偏好的工具自訂主題，然後將變更提交到 AEM 程式碼存放庫，然後進行部署。

本檔案著重於使用快速網站建立工具建立網站。 如果您想概略瞭解網站建立和自訂工作流程，請參閱[AEM快速網站建立歷程](/help/journey-sites/quick-site/overview.md)

## 規劃網站結構 {#structure}

請花點時間提前考慮您網站的目的和規劃內容。 這將推動您設計網站結構的方式。 良好的網站結構可支援網站訪客的輕鬆導覽和內容探索，並支援各種AEM功能，例如[多網站管理和翻譯](/help/sites-cloud/administering/msm-and-translation.md)。

>[!TIP]
>
>[WKND參考網站](https://wknd.site)提供功能齊全的戶外體驗品牌網站的最佳實務實作。 探索該網站，瞭解建置良好的AEM網站是如何建構的。

## 網站範本 {#site-templates}

由於網站結構對於網站的成功非常重要，因此使用預先定義的結構可以很方便地，根據一組現有標準快速部署新網站。 網站範本是一種將基本網站內容結合成方便且可重複使用之封裝的方法。

網站範本通常包含基本網站內容和結構以及網站樣式資訊，以便快速啟動新網站。範本可重複使用且可自訂，因此功能強大。 由於您可以在AEM安裝中使用多個範本，因此可彈性建立不同網站以符合各種業務需求。

>[!TIP]
>
>如需網站範本的詳細資訊，請參閱[網站範本](site-templates.md)。

>[!NOTE]
>
>網站範本與頁面範本不同，請勿混淆二者。網站範本定義網站的整體結構。 頁面範本定義單一頁面的結構和初始內容。

## 建立網站 {#create-site}

使用範本建立網站非常簡單。

1. 登入您的 AEM 製作環境並導覽至 Sites 主控台

   * `https://<your-author-environment>.adobeaemcloud.com/sites.html/content`

1. 選取畫面右上角的「**建立**」並從下拉式清單選取「**來自範本的網站**」。

   ![從範本建立網站](../assets/create-site-from-template.png)

1. 在[建立網站]精靈中，在左側面板中選取現有的範本，或在左側欄頂端的&#x200B;**匯入**&#x200B;上選取要匯入新範本的現有範本。

   ![網站建立精靈](../assets/site-creation-wizard.png)

   1. 如果您選擇匯入，請在檔案瀏覽器中找出您要使用的範本，並選取&#x200B;**上傳**。

   1. 上傳後，範本就會顯示在可用範本清單中。

1. 選取範本時，它會在右欄中顯示範本的相關資訊。 選取您想要的範本後，選取&#x200B;**下一步**。

   ![選取範本](../assets/select-site-template.png)

1. 提供您的網站標題。若省略，可提供網站名稱，或從標題產生。

   * 網站標題顯示在瀏覽器標題列中。
   * 網站名稱成為 URL 的一部分。
   * 網站名稱必須符合[AEM的頁面命名慣例](/help/sites-cloud/authoring/sites-console/organizing-pages.md#page-name-restrictions-and-best-practices)。

1. 選取&#x200B;**建立**，網站是從網站範本建立的。

   ![新網站的詳細資訊](../assets/create-site-details.png)

1. 在出現的確認對話框中，選取「**完成**」。

   ![成功對話框](../assets/success.png)

1. 在網站主控台中，新網站是可見的，且可供導覽以探索其由範本定義的基本結構。

   ![新網站結構](../assets/new-site.png)

內容作者現在可以開始撰寫了！

## 網站自訂 {#site-customization}

如果您的網站需要在可用範本之外進行自訂，您有幾個選項。

* 如果必須調整網站結構或初始內容，[可以自訂網站範本以符合您的需求](site-templates.md)。
* 如果必須調整網站樣式，可以下載[網站主題並加以自訂](/help/journey-sites/quick-site/overview.md)。
* 如果必須調整網站功能，[網站可完全自訂](/help/implementing/developing/introduction/develop-wknd-tutorial.md)。

任何自訂作業都應在開發團隊的支援下進行。
