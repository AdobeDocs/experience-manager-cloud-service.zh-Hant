---
title: 具有OpenAPI功能的Dynamic Media
description: 瞭解重要概念，例如為何將Dynamic Media與OpenAPI功能搭配使用，以及如何啟用它。
role: User
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 0%

---

# 具有OpenAPI功能的Dynamic Media {#new-dynaminc-media-apis-overview}

在當今快節奏的數位世界中，釋放品牌數位資產的全部潛力對於在競爭中保持領先地位至關重要。 整體數位資產管理(DAM)解決方案有助於進行資產治理、促進品牌一致性，並加速內容交付，同時確保品牌完整性和卓越的客戶體驗。

Dynamic Media搭配OpenAPI功能，將DAM置於敏捷且有效率的內容供應鏈生態系統的核心，以確保資產治理和交付。

## 為何要將Dynamic Media與OpenAPI功能搭配使用？ {#new-dynamic-media-api-features}

Dynamic Media搭配OpenAPI功能提供下列主要優點：

* **緊密整合**：具有OpenAPI功能的Dynamic Media提供了一組完整的搜尋和傳送API。 可讓您的開發人員輕鬆進行 [將資產傳送與其應用程式整合](/help/assets/integrate-new-dynamic-media-apis.md). 應用程式包括Adobe以及協力廠商應用程式。 此外，它還提供 [Micro Frontend資產選擇器使用者介面](/help/assets/asset-selector.md) 以搜尋並選取已核准的資產。 此選擇器可以輕鬆地與任何基於JavaScript架構的應用程式(例如React JS、Angular JS和Vanilla JS)整合。

* **集中管理數位資產**： DAM是所有數位資產的單一信任來源。 您的數位資產會在AEM Assets中集中管理，並使用傳送URL參考資料傳送給使用應用程式，而不會複製資產二進位檔案。

* **即時更新**：對DAM中的已核准資產所做的任何變更（包括版本更新和中繼資料修改）都會自動反映在傳送URL中。 透過CDN為Dynamic Media的OpenAPI功能設定了短短的存留時間(TTL)值（10分鐘），不到10分鐘即可顯示所有製作和發佈介面的更新。

* **品牌一致性**：僅限 [品牌核准資產](/help/assets/approved-assets.md) 開放給下游應用程式。 [品牌經理和行銷人員對品牌資產維持嚴格的控制](/help/assets/restrict-assets-delivery.md). 該資產僅供經核准和最新版本的使用，以確保所有管道和應用程式的品牌一致性。

* **網頁最佳化傳遞**：數位資產會以網頁最佳化格式傳送，以增強您數位體驗的核心網頁生態。 這包括支援影像的WebP轉譯、視訊的HLS或DASH通訊協定最適化串流，以及檔案的原始轉譯。

* **動態資產轉換**：我們的系統允許使用稱為影像修飾元的URL引數即時進行影像轉換。 [例如，寬度、高度、旋轉、翻轉、品質、裁切和格式](/help/assets/deliver-assets-apis.md). Dynamic Media的OpenAPI功能也支援影像智慧型裁切功能。 轉換後的轉譯會動態產生，並透過CDN無縫傳送。

* **安全傳送資產**：Dynamic Media搭配OpenAPI功能，提供控制數位資產存取的機制。 您可以指定使用者角色或群組作為要保護之資產的中繼資料，並設定預先定義的時間範圍，在此期間內 [只有授權的使用者才能存取這些資產](/help/assets/restrict-assets-delivery.md). 在限制期間，安全資產的傳送URL無法解析給未獲授權的使用者。

* **有助於做出明智決策的資料深入分析**：除了資產管理和傳遞，它還能擷取CDN資產傳遞的傳遞資料深入分析，讓品牌經理能夠追蹤跨管道的傳遞量度。 它可讓客戶作出資料導向式決策，以持續最佳化資產治理和傳遞策略。

![新的Dynamic Media資料流程圖](assets/dm-openapi-dfd.png)

## 使用OpenAPI功能存取Dynamic Media的必要條件 {#prerequisites-new-dynaminc-media-apis}

若要使用OpenAPI功能存取Dynamic Media，您必須擁有下列專案的授權：

* AEM Assets as a Cloud Service 

* AEM Dynamic Media

## 如何啟用Dynamic Media與OpenAPI功能？ {#enable-new-dynamic-media-apis}

在提交在AEMas a Cloud Service上啟用具有OpenAPI功能的Dynamic Media的請求之前，請確定尚未啟用。 若要確認是否已啟用，請執行下列步驟：

1. 待工程與產品管理確認

若要在AEMas a Cloud Service上啟用具有OpenAPI功能的Dynamic Media，請提交Adobe支援票證，並提供下列詳細資料：

* Cloud Service程式和環境ID

* 透過OpenAPI功能整合以Dynamic Media解決的使用案例詳細資訊

* 要與Dynamic Media與OpenAPI功能整合之下游應用程式的詳細資訊。

  >[!NOTE]
  >
  > 若要與非Adobe應用程式整合，請提供網域名稱以將應用程式託管於白名單中。

* 整合專案中涉及之主要客戶聯絡人的詳細資訊。

提交支援票證後，Adobe會在您的Cloud Service環境中啟用具有OpenAPI功能的Dynamic Media，並共用詳細資訊（例如IMS使用者端ID），以便您繼續整合。

## 深入瞭解主要功能 {#learn-more-key-capabilities}

<table>
<td>
   <a href="/help/assets/approved-assets.md">
   <img alt="在Experience Manager Assets中核准資產" src="./assets/approved-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/approved-assets.md">
      <strong>在Experience Manager Assets中核准資產</strong>
      </a>
   </div>
   <p>
      <em>在AEM Assets中核准資產，以簡化資產管理，確保處理資產的程式受到控制且有效率。</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-new-dynamic-media-apis.md">
   <img alt="將AEM Assets與下游應用程式整合" src="./assets/asset-selector-integration.png" />
   </a>
   <div>
      <a href="/help/assets/integrate-new-dynamic-media-apis.md">
      <strong>將AEM Assets與下游應用程式整合</strong>
      </a>
   </div>
   <p>
      <em>使用搜尋和傳送API或使用Adobe的微前端資產選擇器，將您自己的自訂使用者介面與Experience Manager Assets存放庫整合。</em>
   </p>
</td>
<td>
   <a href="/help/assets/asset-selector.md">
   <img alt="Adobe的資產選擇器" src="./assets/asset-selector-prereqs.png" />
   </a>
   <div>
      <a href="/help/assets/asset-selector.md">
      <strong>Adobe的微前端資產選擇器</strong>
      </a>
   </div>
   <p>
      <em>與AEM Assets存放庫互動的使用者介面可搜尋資產，然後在您的應用程式編寫體驗中使用資產。</em>
   </p>
</td>
</table>
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
      <em>搜尋AEM Assets存放庫中的資產，以便傳送給下游應用程式。</em>
   </p>
</td>
<td>
   <a href="/help/assets/deliver-assets-apis.md">
   <img alt="將資產傳遞至下游應用程式" src="./assets/delivery-url.png" />
   </a>
   <div>
      <a href="/help/assets/deliver-assets-apis.md">
      <strong>將資產傳遞至下游應用程式</strong>
      </a>
   </div>
   <p>
      <em>使用傳送URL將資產傳送至整合的下游應用程式。</em>
   </p>
</td>
<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="限制對Experience Manager中資產的存取" src="./assets/restricted-access.png" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>限制對Experience Manager中資產的存取</strong>
      </a>
   </div>
   <p>
      <em> DAM管理員或品牌管理員可藉由在AEMas a Cloud Service製作執行個體上為已核准的資產設定角色，來限制存取權。</em>
   </p>
</td>
</table>

