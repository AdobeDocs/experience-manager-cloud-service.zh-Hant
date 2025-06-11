---
title: Content Hub 概觀
description: 深入了解 Content Hub、其主要優勢、如何存取，以及如何針對 Content Hub 中的選項提供意見反應。
exl-id: c5908058-f1ad-4aaa-9e8e-c0157e107ed1
source-git-commit: cc6c227a566c4d4fd8c9a20d1bb39020974f494f
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 97%

---

# Content Hub 概觀 {#overview-content-hub}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime 與 Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets 與 Edge Delivery Services 整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>使用者介面可擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>全新</i></sup><a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用 Dynamic Media Prime 與 Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

>[!AVAILABILITY]
>
>現已提供 PDF 格式的 Content Hub 指南。下載完整指南，並使用 Adobe Acrobat AI 助理來回答您的查詢問題。
>
>[!BADGE Content Hub 指南 PDF]{type=Informative url="https://helpx.adobe.com/tw/content/dam/help/en/experience-manager/aem-assets/content-hub.pdf"}

Content Hub 作為 Experience Manager Assets as a Cloud Service 的一部分提供，以實現組織及其業務合作夥伴對品牌內容的大眾化存取。其專注於分配資產以進行大規模啟用，並建立品牌內容變體來提高行銷靈敏度。

## Content Hub 示範 {#content-hub-demo}

>[!IMPORTANT]
>
>[Assets Ultimate](/help/assets/assets-ultimate-overview.md)和Assets as a Cloud Service包含250名Content Hub使用者。 [Assets Prime](/help/assets/assets-prime.md)包含50名Content Hub使用者。

>[!VIDEO](https://video.tv.adobe.com/v/3463712)

## 為什麼要選擇 Content Hub？

Content Hub 提供以下主要優勢：

**在直覺式的入口網站中尋找和共用所有可用的品牌核准資產**

AEM Assets 可作為單一事實來源，而所有核准的資產都會以扁平的階層在 Content Hub 上自動提供，以改善搜尋體驗。

**可設定的使用者介面**

Content Hub 中最常見的屬性 (例如用於搜尋的篩選器、新增或匯入資產時可用的欄位、資產屬性、品牌化橫幅內容) 都是可設定的，管理員可以根據自己的需求輕鬆設定 Content Hub 使用者介面。

**讓非創意人員能夠編輯和混編內容，同時保持品牌形象**

Content Hub 可讓您使用 Adobe Express 來建立新內容 (如果您具有 Adobe Express 權益)。您可以使用易於使用的工具來編輯現有內容、使用範本和品牌元素製作品牌變化版本，並使用 Adobe Firefly 的最新 GenAI 功能來建立新內容。

**取得如何跨團隊使用內容的分析**

[!DNL Content Hub] 提供有關資產的珍貴分析、解決行銷利害關係人經常遇到的挑戰，也就是用於行銷活動、管道和不同區域中之資產的使用統計。透過清楚地了解資產的效能和受歡迎程度，可以提供對於增強使用者體驗來說相當重要的可操作分析。

## 先決條件 {#prerequisites-content-hub}

Content Hub 需要 Experience Manager as a Cloud Service 的生產作者環境，須為 2024.6 版本或更新版本 (最低需為 2024.6.16799 版本)。

## 如何存取 Content Hub？ {#access-content-hub}

[設定 Content Hub](/help/assets/deploy-content-hub.md) 並將使用者新增到 [Content Hub 產品設定檔](/help/assets/deploy-content-hub.md#content-hub-instance-product-profile)後，可以透過以下方式存取 Content Hub：

* 使用以下連結存取 Content Hub：

  `https://experience.adobe.com/#/assets/contenthub`

* 登入 [experience.adobe.com](https://auth.services.adobe.com/en_GB/index.html?callback=https%3A%2F%2Fims-na1.adobelogin.com%2Fims%2Fadobeid%2Fexc_app%2FAdobeID%2Ftoken%3Fredirect_uri%3Dhttps%253A%252F%252Fexperience.adobe.com%252F%2523old_hash%253Dold_hash%253D%252523%25252F%2526from_ims%253Dtrue%253Fclient_id%253Dexc_app%2526api%253Dauthorize%2526scope%253Dab.manage%252Caccount_cluster.read%252Cadditional_info%252Cadditional_info.job_function%252Cadditional_info.projectedProductContext%252Cadditional_info.roles%252CAdobeID%252Cadobeio.appregistry.read%252Cadobeio_api%252Caudiencemanager_api%252Ccreative_cloud%252Cmps%252Copenid%252Corg.read%252Cpps.read%252Cread_organizations%252Cread_pc%252Cread_pc.acp%252Cread_pc.dma_tartan%252Csession%26state%3D%257B%2522jslibver%2522%253A%2522v2-v0.31.0-2-g1e8a8a8%2522%252C%2522nonce%2522%253A%25222316022399331147%2522%257D%26code_challenge_method%3Dplain%26use_ms_for_expiry%3Dtrue&client_id=exc_app&scope=ab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&state=%7B%22jslibver%22%3A%22v2-v0.31.0-2-g1e8a8a8%22%2C%22nonce%22%3A%222316022399331147%22%7D&relay=64da7fa8-cd9e-47cf-9892-7f3ef3092f8c&locale=en_GB&flow_type=token&dctx_id=v%3A2%2Cs%2Cf%2Cb8e64530-b013-11ee-a6c1-e721bdec0171&idp_flow_type=login&response_type=token&profile_filter=%7B%22findFirst%22%3Atrue%2C+%22fallbackToAA%22%3Atrue%2C+%22preferForwardProfile%22%3Atrue%2C+%22searchEntireCluster%22%3Atrue%7D%3B+isOwnedByOrg%28%2776B329395DF155D60A495E2C%40AdobeOrg%27%29&code_challenge_method=plain&redirect_uri=https%3A%2F%2Fexperience.adobe.com%2F%23old_hash%3Dold_hash%3D%2523%252F%26from_ims%3Dtrue%3Fclient_id%3Dexc_app%26api%3Dauthorize%26scope%3Dab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&use_ms_for_expiry=true#/)，然後按一下「**[!UICONTROL 快速存取]**」區段中的「**[!UICONTROL Experience Manager Assets Content Hub]**」：
  ![Content Hub 存取](assets/access-content-hub.png)

* 登入 [experience.adobe.com](https://auth.services.adobe.com/en_GB/index.html?callback=https%3A%2F%2Fims-na1.adobelogin.com%2Fims%2Fadobeid%2Fexc_app%2FAdobeID%2Ftoken%3Fredirect_uri%3Dhttps%253A%252F%252Fexperience.adobe.com%252F%2523old_hash%253Dold_hash%253D%252523%25252F%2526from_ims%253Dtrue%253Fclient_id%253Dexc_app%2526api%253Dauthorize%2526scope%253Dab.manage%252Caccount_cluster.read%252Cadditional_info%252Cadditional_info.job_function%252Cadditional_info.projectedProductContext%252Cadditional_info.roles%252CAdobeID%252Cadobeio.appregistry.read%252Cadobeio_api%252Caudiencemanager_api%252Ccreative_cloud%252Cmps%252Copenid%252Corg.read%252Cpps.read%252Cread_organizations%252Cread_pc%252Cread_pc.acp%252Cread_pc.dma_tartan%252Csession%26state%3D%257B%2522jslibver%2522%253A%2522v2-v0.31.0-2-g1e8a8a8%2522%252C%2522nonce%2522%253A%25222316022399331147%2522%257D%26code_challenge_method%3Dplain%26use_ms_for_expiry%3Dtrue&client_id=exc_app&scope=ab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&state=%7B%22jslibver%22%3A%22v2-v0.31.0-2-g1e8a8a8%22%2C%22nonce%22%3A%222316022399331147%22%7D&relay=64da7fa8-cd9e-47cf-9892-7f3ef3092f8c&locale=en_GB&flow_type=token&dctx_id=v%3A2%2Cs%2Cf%2Cb8e64530-b013-11ee-a6c1-e721bdec0171&idp_flow_type=login&response_type=token&profile_filter=%7B%22findFirst%22%3Atrue%2C+%22fallbackToAA%22%3Atrue%2C+%22preferForwardProfile%22%3Atrue%2C+%22searchEntireCluster%22%3Atrue%7D%3B+isOwnedByOrg%28%2776B329395DF155D60A495E2C%40AdobeOrg%27%29&code_challenge_method=plain&redirect_uri=https%3A%2F%2Fexperience.adobe.com%2F%23old_hash%3Dold_hash%3D%2523%252F%26from_ims%3Dtrue%3Fclient_id%3Dexc_app%26api%3Dauthorize%26scope%3Dab.manage%2Caccount_cluster.read%2Cadditional_info%2Cadditional_info.job_function%2Cadditional_info.projectedProductContext%2Cadditional_info.roles%2CAdobeID%2Cadobeio.appregistry.read%2Cadobeio_api%2Caudiencemanager_api%2Ccreative_cloud%2Cmps%2Copenid%2Corg.read%2Cpps.read%2Cread_organizations%2Cread_pc%2Cread_pc.acp%2Cread_pc.dma_tartan%2Csession&use_ms_for_expiry=true#/)，然後按一下產品切換器中的「**[!UICONTROL Experience Manager Assets Content Hub]**」：
  ![Content Hub 存取方法 3](assets/access-content-hub-alternate.png)

## 提供 Content Hub 意見反應 {#provide-content-hub-feedback}

若要提供任何與產品相關的改進建議，請按一下位於 Content Hub 使用者介面頂端，貴組織名稱旁邊的「**[!UICONTROL 意見反應]**」。

指定主旨、建議的說明，並附上檔案 (如有需要)。按一下「**[!UICONTROL 提交]**」將意見反應提交給 Adobe。

![Content Hub 意見反應](assets/content-hub-feedback.png)

## 為您的團隊設定 Content Hub {#setup-content-hub}

請依照以下步驟為您的團隊設定 Content Hub：

1. [使用 Cloud Manager 為 Experience Manager Assets 啟用 Content Hub](deploy-content-hub.md#enable-content-hub)。

1. [Content Hub 管理員上線](deploy-content-hub.md#onboard-content-hub-administrator)。

1. [新增重要 Content Hub 使用者](deploy-content-hub.md#onboard-content-hub-consumer-users)。

1. [以 DAM 作者或管理員的身分核准 Experience Manager Assets 中的資產](approve-assets.md)。

1. [以管理員的身分為其他使用者設定 Content Hub 使用者介面](configure-content-hub-ui-options.md)。

1. [將 Content Hub 存取權授予團隊中的更多使用者](deploy-content-hub.md#onboard-content-hub-consumer-users)。

1. [存取 Content Hub 入口網站](#access-content-hub)。

1. [提供 Content Hub 意見反應](#provide-content-hub-feedback)。


## 深入了解重要功能 {#key-capabilities-content-module}

<table>
<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="部署 Content Hub" src="./assets/configure-assets.png" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong>設定 Content Hub 使用者介面</strong>
      </a>
   </div>
   <p>
      <em>了解管理員如何設定 Content Hub 使用者介面。</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-content-hub.md">
   <img alt="搜尋 Content Hub 中的可用資產" src="./assets/search.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-content-hub.md">
      <strong>搜尋 Content Hub 中的可用資產</strong>
      </a>
   </div>
   <p>
      <em>了解如何利用各種功能來縮小搜尋結果範圍。</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="使用 Adobe Express 編輯影像" src="./assets/edit-images-content-hub.png" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>使用 Adobe Express 編輯影像</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用 Adobe Express 在 Content Hub 中建立影像變體</em>
   </p>
</td>
</table>
<table>
<td>
   <a href="/help/assets/share-assets-content-hub.md">
   <img alt="共用 Content Hub 中的可用資產" src="./assets/share-assets-banner.png" />
   </a>
   <div>
      <a href="/help/assets/share-assets-content-hub.md">
      <strong>共用 Content Hub 中的可用資產</strong>
      </a>
   </div>
   <p>
      <em>了解如何將一或多項資產作為連結而共用，然後存取它們。</em>
   </p>
</td>
<td>
   <a href="/help/assets/collections-content-hub.md">
   <img alt="在 Content Hub 中管理集合" src="./assets/manage-collection.png" />
   </a>
   <div>
      <a href="/help/assets/collections-content-hub.md">
      <strong>在 Content Hub 中管理集合</strong>
      </a>
   </div>
   <p>
      <em>了解如何使用資產建立集合並加以管理。</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="共用 Content Hub 中的可用資產" src="./assets/asset-insights-banner.jpg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>檢視 Content Hub 中的資產分析</strong>
      </a>
   </div>
   <p>
      <em>內容模組提供資產的珍貴分析，從而解決行銷利害關係人經常遇到的挑戰</em>
   </p>
</td>
</table>
