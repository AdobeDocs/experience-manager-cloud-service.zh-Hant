---
title: AEM Commerce as a Cloud Service快速入門
description: 了解如何將啟用商務的AEM專案部署至執行中的AEM as a Cloud Service環境。 使用AdobeCloud Manager和CI/CD管道的功能，將Venia參考店面建置至執行中的環境。
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: 2afeb12ec7b99da056652fc869da5bc82db30754
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 1%

---

# AEM Commerce as a Cloud Service快速入門 {#start}

若要開始使用AEM Commerce Commerce as a Cloud Service，您的Experience Manager Cloud Service必須布建Commerce Integration Framework(CIF)附加元件。 CIF附加元件是 [AEM Sitesas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html).

## 入門 {#onboarding}

AEM Commerceas a Cloud Service的上線程式為兩個步驟：

1. 啟用AEM Commerceas a Cloud Service，並布建CIF附加元件
2. 將AEM Commerceas a Cloud Service與您的商務解決方案連接

第一步上線步驟由Adobe完成。 如需定價和布建的詳細資訊，您需要聯絡您的銷售代表。

布建CIF附加元件後，該元件即會套用至任何現有的Cloud Manager程式。 如果您沒有Cloud Manager計畫，則需要建立新計畫。 如需詳細資訊，請參閱 [設定您的方案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

第二步是針對每個AEMas a Cloud Service環境提供自助服務。 CIF附加元件初次布建後，您還需要執行一些額外設定。

## 將AEM與Commerce解決方案連結 {#magento}

連接CIF附加元件與 [AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components) 有了商務解決方案，您需要透過Cloud Manager環境變數提供GraphQL端點URL。 變數名稱為 `COMMERCE_ENDPOINT`. 必須配置通過HTTPS的安全連接。

此環境變數會用於兩個位置：

- 從AEM到商務後端的GraphQL呼叫，透過AEM CIF核心元件和客戶專案元件使用的一些通用共用GraphQl用戶端。
- 在變數設定為可用的每個AEM環境上，設定GraphQL代理URL `/api/graphql`. AEM商務製作工具（CIF附加元件）和CIF用戶端元件都會使用此功能。

每個AEMas a Cloud Service環境都可使用不同的GraphQL端點URL。 如此，專案便可將AEM預備環境與商務預備系統和AEM生產環境連結至商務生產系統。 該GraphQL端點必須可公開使用，不支援專用VPN或本地連接。 可選地，可提供驗證頭以使用需要驗證的其他CIF功能。

選用，且僅適用於Adobe Commerce Enterprise / Cloud,CIF附加元件支援為AEM作者使用分段目錄資料。 這需要設定授權Token。 基於安全考量，已設定的授權Token僅可供使用，且用於AEM製作執行個體。 AEM發佈例項無法顯示分階段資料。

有兩個選項可設定端點：

### 透過Cloud Manager UI（預設） {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

您可以使用「環境詳細資訊」頁面上的對話方塊來完成此作業。 查看啟用Commerce的程式的此頁時，如果當前未配置終結點，則將顯示一個按鈕：

![CM環境資訊](/help/commerce-cloud/assets/commerce-cmui.png)

按一下此按鈕會開啟對話方塊：

![CM Commerce端點](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

設定端點後（可選擇性地為分段目錄支援設定驗證Token），端點會顯示在詳細資訊頁面上。 按一下「編輯」圖示會開啟相同的對話方塊，視需要可在其中修改端點。

![CM環境資訊](/help/commerce-cloud/assets/commerce-cmui-done.png)

### 通過Adobe I/OCLI  {#adobe-cli}

要通過Adobe I/OCLI將AEM與商務解決方案連接，請執行以下步驟：

1. 使用Cloud Manager外掛程式取得Adobe I/OCLI

   檢查 [AdobeCloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hant) 如何下載、設定及使用 [Adobe I/OCLI](https://github.com/adobe/aio-cli) 和 [Cloud Manager CLI外掛程式](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. 使用AEMas a Cloud Service程式驗證Adobe I/OCLI

3. 設定 `COMMERCE_ENDPOINT` 變數

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   請參閱 [CLI文檔](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) 以取得詳細資訊。

   商務GraphQL端點URL必須指向商務的GraphQl服務，並使用安全的HTTPS連線。 例如： `https://<yourmagentosystem>/graphql`.

4. 啟用需要驗證的分段目錄功能（可選）

   >[!NOTE]
   >
   >此功能僅適用於Adobe Commerce Enterprise或Cloud Edition。 請參閱 [基於令牌的驗證](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) 以取得詳細資訊。

   設定 `COMMERCE_AUTH_HEADER` Cloud Manager中的機密變數：

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>您可以使用下列命令列出所有Cloud Manager變數，以重複檢查： `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

借此，您就可以使用AEM Commerce as a Cloud Service，並可透過Cloud Manager部署專案。

## 配置儲存和目錄 {#catalog}

CIF附加元件和 [CIF核心元件](https://github.com/adobe/aem-core-cif-components) 可用於連線至不同商務存放區（或存放區檢視等）的多個AEM網站結構。依預設，CIF附加元件會部署，並具有連線至Adobe Commerce預設存放區和目錄(Magento)的預設設定。

依照下列步驟，透過CIFCloud Service設定，針對專案調整此設定：

1. 在AEM中前往「工具 — >Cloud Services-> CIF設定」

2. 選擇要更改的商務配置

3. 透過動作列開啟設定屬性

![CIFCloud Services設定](/help/commerce-cloud/assets/cif-cloud-service-config.png)

可以配置以下屬性：

- GraphQL客戶端 — 選擇配置的GraphQL客戶端以進行商務後端通信。 這通常應保持預設值。
- 儲存檢視 — (Magento)儲存檢視識別碼。 如果為空，則使用預設的商店視圖。
- GraphQL代理路徑 — AEM中的URL路徑GraphQL代理，用於代理向商務後端GraphQL端點的請求。
   >[!NOTE]
   >
   > 在大多數情況下，請設定預設值 `/api/graphql` 不可變更。 只有進階設定（不使用提供的GraphQL代理）才應變更此設定。
- 啟用目錄UID支援 — 在商務後端GraphQL呼叫中，啟用對UID的支援，而非ID。
   >[!NOTE]
   >
   > Adobe Commerce(Magento)2.4.2導入了對UID的支援。僅在您的商務後端支援2.4.2版或更新版本的GraphQL架構時，才啟用此功能。
- 目錄根類別標識符 — 儲存目錄根的標識符（UID或ID）
   >[!CAUTION]
   >
   > 從CIF核心元件2.0.0版開始，即可支援 `id` 已移除並取代為 `uid`. 如果您的專案使用CIF核心元件2.0.0版，則必須啟用目錄UID支援，並使用有效的類別UID作為「目錄根類別識別碼」。

上述組態供參考。 專案應提供自己的設定。

如需使用多個AEM網站結構並結合不同商務目錄的更複雜設定，請參閱 [商務多商店設定](configuring/multi-store-setup.md) 教學課程。

## 其他資源 {#additional-resources}

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [商務多商店設定](configuring/multi-store-setup.md)
