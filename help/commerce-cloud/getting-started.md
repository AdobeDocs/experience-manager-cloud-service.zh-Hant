---
title: 以商務AEM為Cloud Service快速入門
description: 瞭解如何將啟用商務的AEM專案部署至以雲AEM端服務環境執行。 使用Adobe雲管理器和CI/CD管道的功能，將Venia參考店面建置到運行環境。
topics: Commerce
feature: Cloud Manager的Commerce Integration Framework
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
translation-type: tm+mt
source-git-commit: 08e258d4e9cd67de3da2aa57c058036bd104472d
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 2%

---

# 將商務作AEM為Cloud Service入門{#start}

若要開始將AEMCommerce當做Cloud Service，您的Experience Manager Cloud Service必須配備Commerce Integration Framework(CIF)附加元件。 CIF附加元件是位於[AEM Sites之上的附加模組，作為Cloud Service。](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/sites/home.html)

## 入門 {#onboarding}

「商務」AEM作為Cloud Service的登入程式分為兩步：

1. 啟AEM用「Cloud Service」模式並布建CIF附加元件
2. 將商AEM務連結為Cloud Service與您的商務解決方案

第一個上線步驟由Adobe完成。 如需定價和布建的詳細資訊，您必須聯絡銷售代表。

一旦您獲得CIF附加元件的布建，該附加元件將應用於任何現有的Cloud Manager程式。 如果您沒有Cloud Manager計畫，則需要建立新計畫。 有關詳細資訊，請參閱[設定程式](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/setting-up-program.html)。

第二步是將每個環境作為自AEM助服務Cloud Service。 在CIF附加元件初始布建後，您還需要進行一些其它配置。

## 連AEM接商務解決方案{#magento}

要將CIF附加元件和[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)與商務解決方案連接，您需要通過Cloud Manager環境變數提供GraphQL端點URL。 變數名稱為`COMMERCE_ENDPOINT`。 必須配置通過HTTPS的安全連接。

此環境變數用於兩個位置：

- GraphQL呼叫從AEM商務後端，透過CIF核心元件和客戶專案元件使用的一AEM些共用GraphQl用戶端。
- 在`/api/graphql`中設定變AEM數的每個環境上設定GraphQL Proxy URL。 商務製作工AEM具（CIF附加元件）和CIF用戶端元件都會使用此功能。

可將每個GraphQL端點URL用作AEMCloud Service環境。 如此，專案就可將AEM測試環境與商務測試系統及生產AEM環境連結至商務生產系統。 該GraphQL端點必須是公開可用的，不支援專用VPN或本地連接。 可選地，可以提供驗證頭以使用需要驗證的附加CIF功能。

CIF附加元件僅適用於Adobe商務企業／雲端，可選且支援為作者使用分段目錄AEM資料。 這需要設定授權Token。 配置的授權Token僅可供使用，且用於作AEM者例項，以利安全。 AEM發佈例項無法顯示分段資料。

配置端點有兩個選項：

### 透過Cloud Manager UI（預設）{#cm-ui}

您可以使用「環境詳細資訊」頁面上的對話框來完成此操作。 在查看此頁面時，如果當前未配置端點，則將顯示一個按鈕：

![CM環境資訊](/help/commerce-cloud/assets/commerce-cmui.png)

按一下此按鈕會開啟對話方塊：

![CM Commerce端點](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

端點設定後（可選地為分段目錄支援設定驗證Token），端點會顯示在詳細資訊頁面上。 按一下「編輯」(Edit)表徵圖將開啟同一對話框，在該對話框中可以根據需要修改端點。

![CM環境資訊](/help/commerce-cloud/assets/commerce-cmui-done.png)

### 通過Adobe I/OCLI {#adobe-cli}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

要通過AEMAdobe I/OCLI與商務解決方案連接，請執行以下步驟：

1. 使用Cloud Manager插件獲取Adobe I/OCLI

   請查看[AdobeCloud Manager文檔](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)，以瞭解如何下載、設定和使用[Adobe I/OCLI](https://github.com/adobe/aio-cli)和[Cloud Manager CLI plugin](https://github.com/adobe/aio-cli-plugin-cloudmanager)。

2. 將Adobe I/OCLI驗證為AEMCloud Service程式

3. 在Cloud Manager中設定`COMMERCE_ENDPOINT`變數

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   有關詳細資訊，請參見[CLI文檔](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)。

   商務GraphQL端點URL必須指向商務的GraphQl服務，並使用安全的HTTPS連線。 例如：`https://demo.magentosite.cloud/graphql`。

4. 啟用需要驗證的分段目錄功能（可選）

   >[!NOTE]
   >
   >此功能僅適用於Adobe商務企業版或雲端版。 如需詳細資訊，請參閱[Token型驗證](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens)。

   在Cloud Manager中設定`COMMERCE_AUTH_HEADER`密碼變數：

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>您可以使用下列命令列出所有Cloud Manager變數以進行複查：`aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

如此一來，您就可以將「商務」AEM當做Cloud Service使用，並可以透過Cloud Manager部署專案。

## 配置儲存和目錄{#catalog}

CIF附加元件和[CIF核心元件](https://github.com/adobe/aem-core-cif-components)可用於連接至不同商務商店（或商店檢視等）的AEM多個網站結構。依預設，CIF附加元件會部署為預設組態，連接至Adobe商務的預設商店和目錄(Magento)。

此配置可通過CIFCloud Service配置根據以下步驟調整：

1. 轉AEM至「工具」->「Cloud Services」->「CIF配置」

2. 選擇要更改的商務配置

3. 通過操作欄開啟配置屬性

![CIFCloud Services配置](/help/commerce-cloud/assets/cif-cloud-service-config.png)

可以配置以下屬性：

- GraphQL客戶端——選擇已配置的GraphQL客戶端，用於商務後端通信。 這通常應維持在預設值。
- 商店檢視-(Magento)商店檢視識別碼。 如果為空，則使用預設的儲存視圖。
- GraphQL代理路徑——用於代理向商務後端GraphQLAEM端點的請求的URL路徑GraphQL代理。
   >[!NOTE]
   >
   > 在大多數設定中，預設值`/api/graphql`不能更改。 只有不使用提供的GraphQL代理的高級設定才應更改此設定。
- 啟用目錄UID支援——在商務後端GraphQL呼叫中啟用UID支援，而非ID支援。
   >[!NOTE]
   >
   > 對Adobe商務(Magento)2.4.2引入的UID的支援。只有在您的商務後端支援2.4.2版或更新版本的GraphQL架構時，才能啟用此功能。
- 目錄根類別標識符——儲存目錄根的標識符（UID或ID）

上述配置供參考。 專案應提供其專屬的組態。

如需使用多個網站結構AEM並結合不同商務目錄的更複雜設定，請參閱[商務多商店設定](configuring/multi-store-setup.md)教學課程。

## 其他資源 {#additional-resources}

- [AEM 專案原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia Reference Store](https://github.com/adobe/aem-cif-guides-venia)
- [商務多商店設定](configuring/multi-store-setup.md)
