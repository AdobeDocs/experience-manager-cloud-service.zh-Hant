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
source-git-commit: e34592d24c8f6c17e6959db1d5c513feaf6381c8
workflow-type: tm+mt
source-wordcount: '766'
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
可將每個GraphQL端點URL用作AEMCloud Service環境。 如此，專案就可將AEM測試環境與商務測試系統及生產AEM環境連結至商務生產系統。 該GraphQL端點必須是公開可用的，不支援專用VPN或本地連接。 可選地，可以提供驗證頭以使用需要驗證的附加CIF功能。

配置端點有兩個選項：

### 1)透過Cloud Manager UI（預設）

您可以使用「環境詳細資訊」頁面上的對話框來完成此操作。 在查看此頁面時，如果當前未配置端點，則將顯示一個按鈕：

![環保徽章最終實施](/help/commerce-cloud/assets/commerce-cmui.png)

按一下此按鈕會開啟對話方塊：

![環保徽章最終實施](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

設定端點（以及可選地，代號）後，端點會顯示在詳細資料頁面上。 按一下「編輯」(Edit)表徵圖將開啟同一對話框，在該對話框中可以根據需要修改端點。

![環保徽章最終實施](/help/commerce-cloud/assets/commerce-cmui-done.png)

### 2)通過Adobe I/OCLI

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

要通過AEMAdobe I/OCLI與商務解決方案連接，請執行以下步驟：

1. 使用Cloud Manager插件獲取Adobe I/OCLI

   請查看[AdobeCloud Manager文檔](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)，以瞭解如何下載、設定和使用[Adobe I/OCLI](https://github.com/adobe/aio-cli)和[Cloud Manager CLI插件](https://github.com/adobe/aio-cli-plugin-cloudmanager)。

2. 將Adobe I/OCLI驗證為AEMCloud Service程式

3. 在Cloud Manager中設定`COMMERCE_ENDPOINT`變數

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   有關詳細資訊，請參見[CLI文檔](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)。

   商務GraphQL端點URL必須指向商務的GraphQl服務，並使用安全的HTTPS連線。 例如：`https://demo.magentosite.cloud/graphql`。

>[!TIP]
>
>您可以使用下列命令列出所有Cloud Manager變數以進行複查：`aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

如此一來，您就可以將「商務」AEM當做Cloud Service使用，並可以透過Cloud Manager部署專案。

## 啟用需要驗證的功能（可選）{#staging}

>[!NOTE]
>
>此功能僅適用於Magento企業版或Magento雲。

1. 登入Magento並建立整合Token。 如需詳細資訊，請參閱[Token型驗證](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens)。 請確定整合Token僅具有&#x200B;**&#x200B;存取`Content -> Staging`資源的權限。 複製`Access Token`值。

1. 在Cloud Manager中設定`COMMERCE_AUTH_HEADER`密碼變數：

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

   請參閱[將商AEM務與Magento](#magento)連接，瞭解如何為Cloud Manager配置Adobe I/OCLI。

## 第三方商務整合{#integrations}

對於第三方商務整合，需要[API對應層](architecture/third-party.md)才能將商AEM務連結為Cloud Service和CIF核心元件與您的商務系統。 此API對應層通常部署在Adobe I/O Runtime。 請洽詢您的銷售代表，以取得整合併存取Adobe I/O Runtime。
