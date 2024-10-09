---
title: Content Hub概觀
description: 進一步瞭解Content Hub、其主要優點、如何存取該工具，以及如何針對Content Hub中可用的選項提供意見回饋。
exl-id: c5908058-f1ad-4aaa-9e8e-c0157e107ed1
source-git-commit: e3fd0fe2ee5bad2863812ede2a294dd63864f3e2
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 6%

---

# Content Hub概觀 {#overview-content-hub}

| [搜尋最佳實務](/help/assets/search-best-practices.md) | [中繼資料最佳實務](/help/assets/metadata-best-practices.md) | [具有OpenAPI功能的Dynamic Media](/help/assets/dynamic-media-open-apis-overview.md) | [AEM Assets開發人員檔案](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |----|-----|

![Content Hub概觀](assets/content-hub-overview.png)

Content Hub 作為 Experience Manager Assets as a Cloud Service 的一部分提供，以實現組織及其業務合作夥伴對品牌內容的大眾化存取。其著重於大規模散發資產以供啟用，以及建立品牌內內容變體，以提升行銷靈敏度。

## 為何選擇Content Hub？

Content Hub提供下列主要優點：

**尋找並共用直覺式入口網站中可用的所有品牌核准資產**

AEM Assets可作為單一信任來源，而所有已核准的資產都會在Content Hub中以平面階層自動提供，以改善搜尋體驗。

**可設定的使用者介面**

Content Hub中最常見的屬性（例如搜尋的篩選器）、新增或匯入資產時可用的欄位、資產屬性、品牌化的橫幅內容，都是可設定的，管理員可以根據需求輕鬆設定Content Hub使用者介面。

**讓非創意人員編輯與重新混合內容，同時繼續使用品牌**

Content Hub可讓您使用Adobe Express(如果您有Adobe Express許可權)建立新內容。 您可以使用簡單易用的工具編輯現有內容、使用範本和品牌元素產生品牌上的變化，以及從Adobe Firefly使用最新GenAI功能建立新內容。

**深入瞭解跨團隊使用內容的方式**

[!DNL Content Hub]可提供資產的寶貴見解，解決行銷利害關係人經常遇到的共同挑戰 — 行銷活動、管道和不同區域中使用的資產使用統計資料。 透過清楚瞭解資產的效能和受歡迎程度，其提供可操作的深入分析，是提升使用者體驗的必要條件。

## 先決條件 {#prerequisites-content-hub}

Content Hub需要2024.6版或更新版本as a Cloud ServiceExperience Manager的生產製作環境(最低版本為2024.6.16799)。

## 如何存取Content Hub？ {#access-content-hub}

[設定Content Hub](/help/assets/deploy-content-hub.md)並將使用者新增至[Content Hub產品設定檔](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile)後，可以使用下列方式存取Content Hub：

* 使用下列連結存取Content Hub：

  `https://experience.adobe.com/#/assets/contenthub`

* 登入experience.adobe com，然後按一下&#x200B;**[!UICONTROL 快速存取]**&#x200B;區段中可用的&#x200B;**[!UICONTROL Experience Manager Assets Content Hub]**：
  ![Content Hub存取權](assets/access-content-hub.png)

* 登入experience.adobe com，然後按一下產品切換器中可用的&#x200B;**[!UICONTROL Experience Manager Assets Content Hub]**：
  ![Content Hub存取方法3](assets/access-content-hub-alternate.png)



## 提供Content Hub意見回饋 {#provide-content-hub-feedback}

若要建議任何產品相關改良功能，請在Content Hub使用者介面最上方，按一下組織名稱旁的&#x200B;**[!UICONTROL 意見回饋]**。

指定主旨、建議的說明，並視需要附加檔案。 按一下&#x200B;**[!UICONTROL 提交]**&#x200B;提交意見給Adobe。

![Content Hub意見反應](assets/content-hub-feedback.png)

## 為您的團隊設定Content Hub {#setup-content-hub}

請依照下列步驟，為您的團隊設定Content Hub：

1. [使用Cloud Manager](deploy-content-hub.md#enable-content-hub)啟用Experience Manager Assets的Content Hub。

1. [加入Content Hub系統管理員](deploy-content-hub.md#onboard-content-hub-administrator)。

1. [新增金鑰Content Hub使用者](deploy-content-hub.md#onboard-content-hub-consumer-users)。

1. [使用Experience Manager資產核准資產的DAM作者或管理員](approve-assets.md)。

1. [管理員可以為其他使用者設定Content Hub使用者介面](configure-content-hub-ui-options.md)。

1. [將Content Hub存取權授與團隊的其他使用者](deploy-content-hub.md#onboard-content-hub-consumer-users)。

1. [存取Content Hub入口網站](#access-content-hub)

1. [提供Content Hub意見回饋](#provide-content-hub-feedback)。


## 進一步瞭解主要功能 {#key-capabilities-content-module}

<table>
<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="部署 Content Hub" src="./assets/configure-assets.png" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>設定Content Hub使用者介面</strong>
      </a>
   </div>
   <p>
      <em>瞭解管理員如何設定Content Hub使用者介面。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-content-hub.md">
   <img alt="搜尋Content Hub中的可用資產" src="./assets/search.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-content-hub.md">
      <strong>搜尋Content Hub中的可用資產</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何利用各種功能來縮小搜尋結果的範圍。</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="使用 Adobe Express 編輯影像" src="./assets/edit-images-content-hub.png" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>使用Adobe Express編輯影像</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何使用Adobe Express在Content Hub中建立影像的變體</em>
   </p>
</td>
</table>
<table>
<td>
   <a href="/help/assets/share-assets-content-hub.md">
   <img alt="共用Content Hub中的可用資產" src="./assets/share-assets-banner.png" />
   </a>
   <div>
      <a href="/help/assets/share-assets-content-hub.md">
      <strong>在Content Hub中共用可用的資產</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何以連結形式共用一或多個資產，然後存取它們。</em>
   </p>
</td>
<td>
   <a href="/help/assets/collections-content-hub.md">
   <img alt="在 Content Hub 中管理收藏集" src="./assets/manage-collection.png" />
   </a>
   <div>
      <a href="/help/assets/collections-content-hub.md">
      <strong>在Content Hub中管理集合</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何使用資產建立集合，然後管理它們。</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="共用Content Hub中的可用資產" src="./assets/asset-insights-banner.jpg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>在Content Hub中檢視資產分析</strong>
      </a>
   </div>
   <p>
      <em>內容模組提供資產的寶貴見解，解決行銷利害關係人經常遇到的共同挑戰</em>
   </p>
</td>
</table>
