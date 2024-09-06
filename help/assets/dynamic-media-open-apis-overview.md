---
title: 具有OpenAPI功能的Dynamic Media
description: 瞭解重要概念，例如為何將Dynamic Media與OpenAPI功能搭配使用，以及如何啟用它。
role: User
exl-id: 658b6eff-9f5a-4166-9ff6-5dc8eb92ada3
source-git-commit: 1041769d4c1efa4465745a85df65c803939b472b
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 1%

---

# 具有OpenAPI功能的Dynamic Media {#new-dynaminc-media-apis-overview}

在當今快節奏的數位世界中，釋放品牌數位資產的全部潛力對於在競爭中保持領先地位至關重要。 整體數位Assets管理(DAM)解決方案有助於資產控管、促進品牌一致性，並加快內容交付，同時確保品牌完整性和卓越的客戶體驗。

Dynamic Media搭配OpenAPI功能，將DAM置於敏捷且有效率的內容供應鏈生態系統的核心，以確保資產治理和交付。

## 為何要將Dynamic Media與OpenAPI功能搭配使用？ {#dynamic-media-open-api-features}

Dynamic Media搭配OpenAPI功能提供下列主要優點：

* **緊密整合**： Dynamic Media搭配OpenAPI功能，提供完整的搜尋與傳送API集合。 它可讓您的開發人員輕鬆[將資產傳遞與其應用程式](/help/assets/integrate-dynamic-media-open-apis.md)整合。 應用程式包括Adobe以及協力廠商應用程式。 它提供[Micro Frontend資產選擇器使用者介面](/help/assets/overview-asset-selector.md)，以搜尋及選取核准的資產。 此選擇器可以輕鬆地與任何基於JavaScript架構的應用程式(例如React JS、Angular JS和Vanilla JS)整合。

* **數位資產的集中管理**： DAM是所有數位資產的單一信任來源。 您的數位資產會在AEM Assets中集中管理，並使用傳送URL參考資料傳送給使用應用程式，而不會複製資產二進位檔案。

* **即時更新**：對DAM中已核准的資產所做的任何變更（包括版本更新和中繼資料修改）都會自動反映在傳遞URL中。 透過CDN為Dynamic Media的OpenAPI功能設定了短短的存留時間(TTL)值（10分鐘），不到10分鐘即可顯示所有製作和發佈介面的更新。

* **品牌一致性**：只有[品牌核准的資產](/help/assets/approve-assets.md)會公開給下游應用程式。 [品牌管理員和行銷人員對品牌資產有嚴格的控制](/help/assets/restrict-assets-delivery.md)。 該資產僅供經核准和最新版本的使用，以確保所有管道和應用程式的品牌一致性。

* **網頁最佳化傳遞**：數位資產是以網頁最佳化格式傳遞，以增強您數位體驗的核心網頁生態。 這包括支援影像的WebP轉譯、視訊的HLS或DASH通訊協定最適化串流，以及檔案的原始轉譯。

* **動態資產轉換**：我們的系統允許使用稱為影像修飾元的URL引數即時轉換影像。 [例如，寬度、高度、旋轉、翻轉、品質、裁切、格式和智慧型裁切](/help/assets/deliver-assets-apis.md)。 轉換後的轉譯會動態產生，並透過CDN無縫傳送。

* **安全傳送資產**：具有OpenAPI功能的Dynamic Media提供控制數位資產存取權的機制。 您可以將使用者角色或群組指定為要安全保護資產的中繼資料，並設定預先定義的時間範圍，在此期間只有[授權的使用者才能存取這些資產](/help/assets/restrict-assets-delivery.md)。 在限制期間，安全資產的傳送URL無法解析給未獲授權的使用者。

* **做出明智決策的資料深入分析（近期）**：除了資產管理和傳遞之外，它還能擷取CDN資產傳遞的傳遞資料深入分析，讓品牌經理可以追蹤跨管道的傳遞量度。 它可讓客戶作出資料導向式決策，以持續最佳化資產治理和傳遞策略。

![Dynamic Media Open API資料流程圖](assets/dm-openapi-dfd.png)

## 使用OpenAPI功能存取Dynamic Media的必要條件 {#prerequisites-dynaminc-media-open-apis}

若要使用OpenAPI功能存取Dynamic Media，您必須擁有下列專案的授權：

* AEM Assets as a Cloud Service 

* AEM Dynamic Media

## 如何啟用Dynamic Media與OpenAPI功能？ {#enable-dynamic-media-open-apis}

在提交在AEM as a Cloud Service上啟用具有OpenAPI功能的Dynamic Media的請求之前，請確定尚未啟用。

滿足[必要條件](#prerequisites-dynaminc-media-open-apis)後，如果在您的AEM as a Cloud Service執行個體上啟用具有OpenAPI功能的Dynamic Media，則存放庫中的每個已核准資產都會有一個傳送URL。 如需如何複製傳遞URL的詳細資訊，請參閱[複製已核准資產的傳遞URL](approve-assets.md#copy-delivery-url-approved-assets) 。 Adobe建議使用此方法，在提交支援票證以啟用之前，確認已在AEM as a Cloud Service上啟用具有OpenAPI功能的Dynamic Media。

若要在AEM as a Cloud Service上啟用具有OpenAPI功能的Dynamic Media，請提交Adobe支援票證，並提供下列詳細資料：

* Cloud Service程式和環境ID

* 透過OpenAPI功能整合以Dynamic Media解決的使用案例詳細資訊。

* 要與Dynamic Media與OpenAPI功能整合之下游應用程式的詳細資訊。

  >[!NOTE]
  >
  > 若要與非Adobe應用程式整合，請提供網域名稱以將應用程式託管於白名單中。

* 整合專案中涉及之主要客戶聯絡人的詳細資訊。

* 主要Adobe帳戶團隊成員的清單（電子郵件）。

提交支援票證後，Adobe會在您的Cloud Service環境中啟用具有OpenAPI功能的Dynamic Media，並共用詳細資訊（例如IMS使用者端ID），以便您繼續整合。

>[!NOTE]
>
>從任何內容套件中排除`/conf/global/settings/dam/assets-configurations/assetdelivery`，以避免停用OpenAPI功能的Dynamic Media。

## 深入瞭解主要功能 {#learn-more-key-capabilities}

<table>
<td>
   <a href="/help/assets/approve-assets.md">
   <img alt="在Experience Manager Assets中核准資產" src="./assets/approved-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/approve-assets.md">
      <strong>在Experience Manager Assets中核准資產</strong>
      </a>
   </div>
   <p>
      <em>在AEM Assets中核准資產，以簡化資產管理，確保處理資產的程式受到控制且有效率。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-dynamic-media-open-apis.md">
   <img alt="將AEM Assets與下游應用程式整合" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-dynamic-media-open-apis.md">
      <strong>整合AEM Assets與下游應用程式</strong>
      </a>
   </div>
   <p>
      <em>使用搜尋和傳遞API將您自己的自訂使用者介面與Experience Manager Assets存放庫整合，或使用Adobe的微前端資產選擇器。</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="Adobe的資產選擇器" src="./assets/asset-selector-prereqs.png" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>Adobe的微前端資產選擇器</strong>
      </a>
   </div>
   <p>
      <em>與AEM Assets存放庫互動的使用者介面可搜尋資產，然後將其用於您的應用程式編寫體驗。</em>
   </p>
</td>
</table>
<table>



<table>
<td>
   <a href="/help/assets/search-assets-api.md">
   <img alt="搜尋資產Experience Manager Assets存放庫" src="./assets/search-assets-api-overview.png" />
   </a>
   <div>
      <a href="/help/assets/search-assets-api.md">
      <strong>在Experience Manager Assets存放庫中搜尋資產</strong>
      </a>
   </div>
   <p>
      <em>搜尋AEM Assets存放庫中的資產，以便傳遞至下游應用程式。</em>
   </p>
</td>
<td>
   <a href="/help/assets/deliver-assets-apis.md">
   <img alt="將資產傳遞至下游應用程式" src="./assets/delivery-url.png" />
   </a>
   <div>
      <a href="/help/assets/deliver-assets-apis.md">
      <strong>傳遞資產給下游應用程式</strong>
      </a>
   </div>
   <p>
      <em>使用傳遞URL將資產傳遞給整合的下游應用程式。</em>
   </p>
</td>
<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="限制對Experience Manager中資產的存取" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>限制對Experience Manager</strong>中資產的存取
      </a>
   </div>
   <p>
      <em> DAM管理員或品牌管理員在AEM as a Cloud Service作者執行個體上設定已核准資產的角色，以限制存取權。</em>
   </p>
</td>

</table>
<table>
<td>
   <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
   <img alt="將遠端 AEM Assets 與 AEM Sites 整合" src="./assets/connected-assets-rdam.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
      <strong>將遠端AEM Assets與AEM Sites整合</strong>
      </a>
   </div>
   <p>
      <em>瞭解如何將遠端AEM Assets與AEM Sites環境整合。</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media-open-apis-faqs.md">
   <img alt="具有OpenAPI功能的Dynamic Media常見問題" src="./assets/dynamic-media-faqs.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-faqs.md">
      <strong>具有OpenAPI功能的Dynamic Media常見問題</strong>
      </a>
   </div>
   <p>
      <em>透過OpenAPI功能取得最常問Dynamic Media問題的回應。</em>
   </p>
</td>
<td>
   <a href="/help/assets/configure-custom-domain.md">
   <img alt="設定自訂網域" src="./assets/configure-custom-domain.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-custom-domain.md">
      <strong>設定自訂網域</strong>
      </a>
   </div>
   <p>
      <em>雖然AEM as a Cloud Service隨附預設網域，但您可以視需求加以自訂。</em>
   </p>
</td>

</table>
