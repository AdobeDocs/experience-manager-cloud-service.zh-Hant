---
title: AEM Commerceas a Cloud Service快速入門
description: 瞭解如何將具有Commerce功能的AEM專案部署至執行中的AEM as a Cloud Service環境。 使用Adobe Cloud Manager和CI/CD管道的功能，以便您建立Venia參考店面到執行中的環境。
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 3%

---

# AEM Commerceas a Cloud Service快速入門 {#start}

若要開始使用AEM Commerceas a Cloud Service，您的Experience Manager Cloud Service必須布建Commerce Integration Framework (CIF)附加元件。 CIF附加元件是上方的額外模組 [AEM Sitesas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/home.html).

## 上線 {#onboarding}

AEM Commerceas a Cloud Service入門有兩個步驟：

1. 啟用AEM Commerceas a Cloud Service並布建CIF附加元件
2. 將AEM Commerceas a Cloud Service與您的商務解決方案連線

第一個入門步驟透過Adobe完成。 如需定價和布建的詳細資訊，請洽詢您的銷售代表。

布建CIF附加元件後，它會套用至任何現有的Cloud Manager方案。 如果您沒有Cloud Manager計畫，則必須建立一個計畫。 如需詳細資訊，請參閱 [設定您的程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/getting-started/program-setup.html).

第二步是每個AEMas a Cloud Service環境的自助服務。 在初始布建CIF附加元件後，您必須進行一些其他設定。

## 將AEM與商務解決方案連線 {#solution}

若要連線CIF附加元件和 [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) 使用商務解決方案時，您必須透過Cloud Manager環境變數提供GraphQL端點URL。 變數名稱為 `COMMERCE_ENDPOINT`. 必須設定透過HTTPS的安全連線。

此環境變數用於兩個位置：

- GraphQL會透過AEM CIF核心元件和客戶專案元件使用的一些常見可共用GraphQl使用者端，從AEM呼叫商務後端。
- 在設定變數的每個AEM環境中設定GraphQL Proxy URL，網址為 `/api/graphql`. 此URL由AEM Commerce編寫工具（CIF附加元件）和CIF使用者端元件使用。

不同的GraphQL端點URL可用於每個AEMas a Cloud Service環境。 如此一來，專案可將AEM中繼環境與商務中繼系統和AEM生產環境連線到商務生產系統。 GraphQL端點必須是公開可用的，不支援私人VPN或本機連線。 可選擇性地提供驗證標頭，以使用需要驗證的其他CIF功能。

CIF附加元件可選擇性支援AEM作者使用分階段目錄資料，且僅適用於Adobe Commerce Enterprise/Cloud。 此資料需要您設定授權標頭。 基於安全理由，此標頭僅適用於AEM編寫執行個體。 AEM發佈執行個體無法顯示分段資料。

有兩個選項可設定端點：

### 透過Cloud Manager使用者介面（預設） {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

此設定可使用「環境詳細資訊」頁面上的對話方塊來完成。 檢視已啟用Commerce的程式的此頁面時，如果目前未設定端點，則會顯示按鈕：

![CM環境資訊](/help/commerce-cloud/assets/commerce-cmui.png)

按一下此按鈕會開啟一個對話方塊：

![CM商務端點](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

設定了分段目錄支援的端點及授權標頭（可選）後，端點會顯示在詳細資訊頁面上。 按一下「編輯」圖示以開啟同一個對話方塊，您可以視需要在此編輯端點。

![CM環境資訊](/help/commerce-cloud/assets/commerce-cmui-done.png)

### 透過Adobe I/OCLI  {#adobe-cli}

若要透過Adobe I/OCLI連線AEM與商務解決方案，請遵循下列步驟：

1. 使用Cloud Manager外掛程式取得Adobe I/OCLI

   檢查 [AdobeCloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html) 下載、設定及使用 [ADOBE I/OCLI](https://github.com/adobe/aio-cli) 使用 [Cloud Manager CLI外掛程式](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. 使用AEMas a Cloud Service程式驗證Adobe I/OCLI

3. 設定 `COMMERCE_ENDPOINT` Cloud Manager中的變數

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   另請參閱 [CLI檔案](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) 以取得詳細資訊。

   商務GraphQL端點URL必須指向商務的GraphQl服務，並使用安全的HTTPS連線。 例如：`https://<yourcommercesystem>/graphql`。

4. 啟用需要驗證的階段式目錄功能（選擇性）

   >[!NOTE]
   >
   >此功能僅適用於Adobe Commerce Enterprise或Cloud Edition。 另請參閱 [權杖型驗證](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) 以取得詳細資訊。

   設定 `COMMERCE_AUTH_HEADER` Cloud Manager中的密碼變數：

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>您可以使用以下命令列出所有Cloud Manager變數來仔細檢查： `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

您已準備好使用AEM Commerceas a Cloud Service，並且可以透過Cloud Manager部署您的專案。

## 設定存放區和目錄 {#catalog}

CIF附加元件和 [CIF Core Components](https://github.com/adobe/aem-core-cif-components) 可用於連線至不同商業商店（或商店檢視等）的多個AEM網站結構。 根據預設，CIF附加元件會以預設設定部署，並連線至Adobe Commerce的預設存放區和目錄。

您可以按照以下步驟使用CIFCloud Service設定來調整專案的此設定：

1. 在AEM中，前往「工具 — >Cloud Services-> CIF設定」。

2. 選取您要變更的商務設定。

3. 透過動作列開啟設定屬性。

![CIFCloud Services設定](/help/commerce-cloud/assets/cif-cloud-service-config.png)

可設定下列屬性：

- GraphQL使用者端 — 選取已設定的GraphQL使用者端以進行商務後端通訊。 此使用者端通常應維持預設值。
- 存放區檢視 — 存放區檢視識別碼。 如果為空，則使用預設存放區檢視。
- GraphQL Proxy路徑 — AEM中的GraphQL Proxy用來將請求代理至商務後端GraphQL端點的URL路徑。
  >[!NOTE]
  >
  > 在大多數設定中，預設值 `/api/graphql` 不可變更。 只有不使用所提供的GraphQL Proxy的進階設定才應變更此設定。
- 啟用目錄UID支援 — 在商務後端GraphQL呼叫中啟用UID而非ID支援。
  >[!NOTE]
  >
  > Adobe Commerce 2.4.2匯入UID支援。只有當您的商務後端支援2.4.2版或更新版本的GraphQL結構描述時，才啟用UID。
- 目錄根類別識別碼 — 商店目錄根的識別碼（UID或ID）
  >[!CAUTION]
  >
  > 從CIF Core Components 2.0.0版開始，支援 `id` 已移除並取代為 `uid`. 如果您的專案使用CIF核心元件2.0.0版，您必須啟用目錄UID支援，並使用有效的類別UID作為「目錄根類別識別碼」。

以上所示的設定僅供參考。 專案應提供自己的設定。

如需更複雜的設定，搭配使用多個AEM網站結構與不同的商務目錄，請參閱 [Commerce多商店設定](configuring/multi-store-setup.md) 教學課程。

## 其他資源 {#additional-resources}

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
- [Commerce多商店設定](configuring/multi-store-setup.md)
- [多重Commerce系統設定](configuring/multiple-commerce-systems-setup.md)

