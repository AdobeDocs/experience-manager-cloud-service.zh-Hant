---
title: Commerce AEMas a Cloud Service入門
description: 瞭解如何將支援商業的項AEM目部署到以雲服務AEM環境運行的項目。 使用Adobe雲管理器和CI/CD管道的功能，將Venia參考庫構建到運行環境。
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: 05a412519a2d2d0cba0a36c658b8fed95e59a0f7
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 1%

---

# Commerce AEMas a Cloud Service入門 {#start}

要開始使AEM用Commerceas a Cloud Service，您的Experience Manager Cloud Service需要配置Commerce Integration Framework(CIF)附加模組。 CIF附加模組位於 [AEM Sitesas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html)。

## 入門 {#onboarding}

Commerce AEMas a Cloud Service的登陸過程分為兩步：

1. 啟AEM用Commerceas a Cloud Service並設定CIF載入項
2. 將AEMCommerceas a Cloud Service與您的商業解決方案連接

第一步是Adobe。 有關定價和資源調配的詳細資訊，您需要聯繫您的銷售代表。

一旦您配置了CIF附加程式，它將應用於任何現有的雲管理器程式。 如果您沒有雲管理器程式，則需要建立新程式。 有關詳細資訊，請參閱 [設定程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html)。

第二步是針對每個as a Cloud Service環境進AEM行自助服務。 在初始配置CIF附加模組後，您需要執行一些其他配置。

## 與商AEM務解決方案連接 {#solution}

連接CIF附加模組和 [AEMCIF核心元件](https://github.com/adobe/aem-core-cif-components) 通過商業解決方案，您需要通過Cloud Manager環境變數提供GraphQL終結點URL。 變數名稱為 `COMMERCE_ENDPOINT`。 必須配置通過HTTPS的安全連接。

此環境變數用於兩個位置：

- GraphQL通過AEMCIF核心元件和客戶項目元件使用的一些常用可共用的GraphQl客戶端從商業後端調AEM用。
- 在變數設定可用的每個AEM環境上設定GraphQL代理URL `/api/graphql`。 商業創作工AEM具（CIF附加）和CIF客戶端元件使用此功能。

每個as a Cloud Service環境都可使用不同的GraphQL終結點URLAEM。 這樣，項目就可AEM以將登台環境與商業登台AEM系統和生產環境連接到商業生產系統。 該GraphQL終結點必須可公開使用，不支援專用VPN或本地連接。 可選地，可以提供驗證報頭以使用需要驗證的附加CIF功能。

CIF附加模組對Adobe Commerce企業/雲是可選的且僅支援為作者使用分階段編AEM錄資料。 這要求配置授權令牌。 配置的授權令牌僅可用，出於安AEM全原因，在作者實例上使用。 發AEM布實例無法顯示暫存資料。

配置端點有兩個選項：

### 通過Cloud Manager UI（預設） {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

可以使用「環境詳細資訊」(Environment Details)頁面上的對話框來完成此操作。 查看啟用Commerce的程式的此頁時，如果當前未配置終結點，則將顯示按鈕：

![CM環境資訊](/help/commerce-cloud/assets/commerce-cmui.png)

按一下此按鈕將開啟一個對話框：

![CM Commerce終結點](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

設定終結點（可選地，是用於轉移目錄支援的驗證令牌）後，該終結點將顯示在詳細資訊頁上。 按一下「編輯」(Edit)表徵圖將開啟同一對話框，在該對話框中，如果需要，可以修改端點。

![CM環境資訊](/help/commerce-cloud/assets/commerce-cmui-done.png)

### 通過Adobe I/OCLI  {#adobe-cli}

要通AEM過Adobe I/OCLI連接Commerce解決方案，請執行以下步驟：

1. 使用Cloud Manager插件獲取Adobe I/OCLI

   檢查 [Adobe雲管理器文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hant) 如何下載、設定和使用 [Adobe I/OCLI](https://github.com/adobe/aio-cli) 和 [Cloud Manager CLI插件](https://github.com/adobe/aio-cli-plugin-cloudmanager)。

2. 使用as a Cloud Service程式驗證Adobe I/OAEM CLI

3. 設定 `COMMERCE_ENDPOINT` 雲管理器中的變數

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   請參閱 [CLI文檔](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) 的雙曲餘切值。

   商業GraphQL終結點URL必須指向商業的GraphQl服務，並使用安全的HTTPS連接。 例如： `https://<yourcommercesystem>/graphql`。

4. 啟用需要身份驗證的分段目錄功能（可選）

   >[!NOTE]
   >
   >此功能僅適用於Adobe Commerce企業版或雲版。 請參閱 [基於令牌的身份驗證](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) 的雙曲餘切值。

   設定 `COMMERCE_AUTH_HEADER` 雲管理器中的秘密變數：

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>可以使用以下命令列出所有Cloud Manager變數以進行雙重檢查： `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

利用此功能，您可以使AEM用Commerceas a Cloud Service，並可以通過雲管理器部署您的項目。

## 配置儲存和目錄 {#catalog}

CIF附加程式和 [CIF核心元件](https://github.com/adobe/aem-core-cif-components) 可以用於連接到AEM不同商業商店（或商店視圖等）的多個站點結構。預設情況下，CIF載入項部署時使用連接到Adobe Commerce預設商店和目錄的預設配置。

通過CIFCloud Service配置，可以根據項目調整此配置，步驟如下：

1. 轉AEM至工具 — >Cloud Services-> CIF配置

2. 選擇要更改的商業配置

3. 通過操作欄開啟配置屬性

![CIFCloud Services配置](/help/commerce-cloud/assets/cif-cloud-service-config.png)

可以配置以下屬性：

- GraphQL客戶端 — 選擇已配置的GraphQL客戶端以進行商務後端通信。 通常應保持預設狀態。
- 儲存視圖 — 儲存視表徵圖識符。 如果為空，則使用預設儲存視圖。
- GraphQL代理路徑 — 用於代理向商業後端GraphQL終結點AEM的請求的URL路徑GraphQL代理。
   >[!NOTE]
   >
   > 在大多數設定中，預設值 `/api/graphql` 不能更改。 只有不使用提供的GraphQL代理的高級設定才應更改此設定。
- 啟用目錄UID支援 — 在商務後端GraphQL調用中啟用對UID的支援，而不是ID的支援。
   >[!NOTE]
   >
   > UID支援在Adobe Commerce2.4.2推出。僅當您的商業後端支援2.4.2版或更高版本的GraphQL架構時才啟用此功能。
- 目錄根類別標識符 — 儲存目錄根的標識符（UID或ID）
   >[!CAUTION]
   >
   > 從CIF核心元件2.0.0版開始，支援 `id` 已移除並替換為 `uid`。 如果項目使用CIF核心元件2.0.0版，則必須啟用目錄UID支援並使用有效的類別UID作為「目錄根類別標識符」。

上面所示的配置可供參考。 項目應提供自己的配置。

有關使用多個站點結構並AEM結合不同商業目錄的更複雜的設定，請參閱 [Commerce多商店設定](configuring/multi-store-setup.md) 教程。

## 其他資源 {#additional-resources}

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [韋尼AEM亞引用儲存](https://github.com/adobe/aem-cif-guides-venia)
- [Commerce多商店設定](configuring/multi-store-setup.md)
