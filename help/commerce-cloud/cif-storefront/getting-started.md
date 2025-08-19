---
title: AEM Commerce as a Cloud Service快速入門
description: 瞭解如何使用Adobe Experience Manager Cloud Manager、CI/CD管道和Venia參考店面部署Adobe (AEM)商務專案。
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Experience Manager as a Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
role: Admin
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 1%

---


# AEM Commerce as a Cloud Service快速入門 {#start}

若要開始使用Adobe Experience Manager (AEM) Commerce as a Cloud Service，您的Experience Manager Cloud Service必須布建Commerce integration framework (CIF)附加元件。 CIF附加元件是在[AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)之上的額外模組。

>[!TIP]
>
>**您考慮過Edge Delivery Services嗎？**
>
>Edge Delivery Services是Adobe建立店面的首選解決方案。 如需詳細資訊，請參閱檔案[簡介和概觀](/help/commerce-cloud/introduction.md)。

## 上線 {#onboarding}

AEM Commerce as a Cloud Service的上線流程分為兩個步驟：

1. 啟用AEM Commerce as a Cloud Service，並布建CIF附加元件
1. 將AEM Commerce as a Cloud Service與您的商務解決方案連結

Adobe已完成第一個入門步驟。 如需有關定價和布建的詳細資訊，請洽詢您的銷售代表。

布建CIF附加元件後，它會套用至任何現有的Cloud Manager方案。 如果您沒有Cloud Manager計畫，則必須建立一個計畫。 如需詳細資訊，請參閱[設定您的程式。](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/program-setup.html)

第二步是每個AEM as a Cloud Service環境的自助服務。 在CIF附加元件初始布建後，您必須進行一些其他設定。

## 將AEM與Commerce解決方案連線 {#solution}

若要將CIF附加元件和[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)與商務解決方案連線，您必須透過Cloud Manager環境變數提供GraphQL端點URL。 變數名稱為`COMMERCE_ENDPOINT`。 必須設定透過HTTPS的安全連線。

此環境變數用於兩個位置：

* GraphQL會透過AEM AEM核心元件和客戶專案元件使用的一些常見可共用GraphQl使用者端，從CIF呼叫商務後端。
* 在每個GraphQL環境中設定AEM Proxy URL，變數可在`/api/graphql`取得。 此URL供AEM Commerce編寫工具(CIF附加元件)和CIF使用者端元件使用。

每個GraphQL環境可以使用不同的AEM as a Cloud Service端點URL。 如此一來，專案就可以將AEM測試環境與商務測試系統和AEM生產環境連線到商務生產系統。 GraphQL端點必須是公開可用的，不支援私人VPN或本機連線。 可選擇提供驗證標頭，以使用需要驗證的其他CIF功能。

CIF附加元件可選擇性支援對Adobe Commerce Enterprise/Cloud作者使用分階段目錄資料，且僅適用於AEM Enterprise/Cloud。 此資料需要您設定授權標頭。 基於安全考量，此標題僅適用於AEM Author執行個體。 AEM發佈執行個體無法顯示分段資料。

有兩個選項可設定端點：

### 透過Cloud Manager使用者介面（預設） {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

此設定可使用環境詳細資訊頁面上的對話方塊完成。 檢視啟用Commerce的程式的此頁面時，如果目前未設定端點，則會顯示按鈕：

![CM環境資訊](/help/commerce-cloud/cif-storefront/assets/commerce-cmui.png)

按一下此按鈕會開啟對話方塊：

![CM Commerce端點](/help/commerce-cloud/cif-storefront/assets/commerce-cm-endpoint.png)

在設定分段目錄支援的端點及授權標頭（可選）後，端點會顯示在詳細資訊頁面上。 按一下「編輯」圖示，開啟相同的對話方塊，您可在其中編輯端點（如有必要）。

![CM環境資訊](/help/commerce-cloud/cif-storefront/assets/commerce-cmui-done.png)

### 透過Adobe I/O CLI  {#adobe-cli}

若要透過AEM CLI將Adobe I/O與商務解決方案連線，請遵循下列步驟：

1. 使用Cloud Manager外掛程式取得Adobe I/O CLI。

   * 請檢視[Adobe Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)，瞭解如何下載、設定和使用[Adobe I/O CLI](https://github.com/adobe/aio-cli)搭配[Cloud Manager CLI外掛程式。](https://github.com/adobe/aio-cli-plugin-cloudmanager)

1. 使用AEM as a Cloud Service程式驗證Adobe I/O CLI。

1. 在Cloud Manager中設定`COMMERCE_ENDPOINT`變數。

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   * 如需詳細資訊，請參閱[CLI檔案](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)。

   * 商務GraphQL端點URL必須指向商務的GraphQl服務並使用安全的HTTPS連線。 例如：`https://<yourcommercesystem>/graphql`。

1. 啟用需要驗證的階段式目錄功能（選擇性）。

   >[!NOTE]
   >
   >此功能僅適用於Adobe Commerce Enterprise或Cloud版。 如需詳細資訊，請參閱[權杖型驗證](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens)。

   * 在Cloud Manager中設定`COMMERCE_AUTH_HEADER`密碼變數：

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>您可以使用以下命令列出所有Cloud Manager變數來仔細檢查： `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

您已準備好使用AEM Commerce as a Cloud Service，並可透過Cloud Manager部署您的專案。

## 設定存放區和目錄 {#catalog}

CIF附加元件和[CIF核心元件](https://github.com/adobe/aem-core-cif-components)可用於連線至不同商務商店（或商店檢視等）的多個AEM網站結構。 依預設，CIF附加元件會以連線到Adobe Commerce預設存放區和目錄的預設設定進行部署。

您可以透過CIF Cloud Service設定，依照下列步驟針對專案調整此設定：

1. 在AEM中，前往「工具>雲端服務> CIF設定」 。

1. 選取您要變更的商務設定。

1. 透過動作列開啟設定屬性。

![CIF Cloud Services設定](/help/commerce-cloud/cif-storefront/assets/cif-cloud-service-config.png)

可以設定下列屬性：

* GraphQL使用者端 — 選取已設定的GraphQL使用者端以進行商務後端通訊。 此使用者端通常應維持預設值。
* 存放區檢視 — 存放區檢視識別碼。 如果空白，則使用預設存放區檢視。
* GraphQL Proxy路徑 — AEM中的GraphQL Proxy用來將請求代理至商務後端GraphQL端點的URL路徑。
  >[!NOTE]
  >
  > 在大多數設定中，不可變更預設值`/api/graphql`。 只有未使用所提供GraphQL Proxy的進階設定，才應變更此設定。
* 啟用目錄UID支援 — 在商務後端GraphQL呼叫中啟用對UID的支援，而非ID。
  >[!NOTE]
  >
  > Adobe Commerce 2.4.2引進了對UID的支援。只有當您的商務後端支援2.4.2版或更新版本的GraphQL結構描述時，才啟用UID。
* 目錄根類別識別碼 — 商店目錄根的識別碼(UID或ID)
  >[!CAUTION]
  >
  > 從CIF核心元件2.0.0版開始，已移除對`id`的支援，並取代為`uid`。 如果您的專案使用CIF核心元件2.0.0版，您必須啟用目錄UID支援，並使用有效類別UID做為「目錄根類別識別碼」。

以上所示的設定可供參考。 專案應提供自己的設定。

如需更複雜的設定，請使用多個AEM網站結構搭配不同的商務目錄，請參閱[Commerce多商店設定](/help/commerce-cloud/cif-storefront/configuring/multi-store-setup.md)教學課程。

## 其他資源 {#additional-resources}

* [AEM專案原型](https://github.com/adobe/aem-project-archetype)
* [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
* [Commerce多商店設定](/help/commerce-cloud/cif-storefront/configuring/multi-store-setup.md)
* [多個Commerce系統設定](/help/commerce-cloud/cif-storefront/configuring/multiple-commerce-systems-setup.md)
