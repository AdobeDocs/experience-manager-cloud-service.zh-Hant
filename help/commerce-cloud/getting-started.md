---
title: AEM Commerce as a Cloud Service快速入門
description: 瞭解如何將啟用商務的AEM專案部署至執行中的AEM做為雲端服務環境。 使用Adobe Cloud Manager的功能和CI/CD管道，將Venia參考店面建置至執行環境。
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: cloud-service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
translation-type: tm+mt
source-git-commit: 7a26596b00f276404934e467490ff79d08b0e1d0
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 2%

---


# AEM Commerce as a Cloud Service {#start}快速入門

若要以雲端服務的形式開始使用AEM Commerce，您的Experience Manager Cloud服務必須配備Commerce Integration Framework(CIF)附加元件。 CIF附加元件是位於[AEM Sites上的額外模組，做為雲端服務](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/sites/home.html)。

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

## 入門 {#onboarding}

AEM Commerce即雲端服務的上線程式是兩個步驟：

1. 啟用AEM Commerce即雲端服務，並布建CIF附加元件
2. 將AEM Commerce以雲端服務方式與您的Magento環境連接

第一步由Adobe完成。 您需要提供IMS組織、GraphQL端點URL等資訊。 作為布建過程的一部分。 如需定價和布建的詳細資訊，您必須聯絡銷售代表。

一旦您獲得CIF附加元件的布建，該附加元件將應用於任何現有的Cloud Manager程式。 如果您沒有Cloud Manager計畫，則需要建立新計畫。 有關詳細資訊，請參閱[設定程式](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/setting-up-program.html)。

第二個步驟是針對每個AEM提供自助服務，做為雲端服務環境。 在CIF附加元件初始布建後，您還需要進行一些其它配置。

## 將AEM Commerce與Magento {#magento}連接

要將CIF附加元件和[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)與Magento環境連接，您需要通過Cloud Manager環境變數提供Magento GraphQL端點URL。 變數名稱為`COMMERCE_ENDPOINT`。 必須配置通過HTTPS的安全連接。
每個AEM都可以使用不同的Magento GraphQL端點URL做為雲端服務環境。 如此，專案就可將AEM測試環境與Magento測試系統和AEM生產環境連接至Magento生產系統。 Magento GraphQL端點必須是公開可用的，不支援專用VPN或本地連接。

若要將AEM Commerce與Magento連線，請依照下列步驟進行：

1. 使用Cloud Manager增效模組取得Adobe I/O CLI

   請查看[Adobe Cloud Manager檔案](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)，瞭解如何下載、設定及使用[Adobe I/O CLI](https://github.com/adobe/aio-cli)和[ Cloud Manager CLI外掛程式](https://github.com/adobe/aio-cli-plugin-cloudmanager)。

2. 以AEM作為雲端服務程式驗證CLI

3. 在Cloud Manager中設定`COMMERCE_ENDPOINT`變數

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   有關詳細資訊，請參見[CLI文檔](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid)。

   Magento GraphQL端點URL必須指向Magento的GraphQl服務，並使用安全的HTTPS連接。 例如：`https://demo.magentosite.cloud/graphql`。

>[!TIP]
>
>您可以使用下列命令列出所有Cloud Manager變數以進行複查：`aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!NOTE]
>
>或者，您也可以使用[Cloud Manager API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)來設定Cloud Manager變數。

有了這項功能，您就可以將AEM Commerce當做雲端服務使用，而且可以透過Cloud Manager部署專案。

## 啟用分段目錄功能（可選）{#staging}

>[!NOTE]
>
>此功能僅適用於Magento Enterprise Edition或Magento Cloud。

1. 登入Magento並建立整合Token。 如需詳細資訊，請參閱[Token型驗證](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens)。 請確定整合Token僅具有&#x200B;**&#x200B;存取`Content -> Staging`資源的權限。 複製`Access Token`值。

1. 在Cloud Manager中設定`COMMERCE_AUTH_HEADER`密碼變數：

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization Bearer: <Access Token>"
   ```

   請參閱[將AEM Commerce與Magento](#magento)連接，以瞭解如何設定Cloud Manager的Adobe I/O CLI。

## 第三方商務整合{#integrations}

對於第三方商務整合，需要[API對應層](architecture/third-party.md)才能將AEM Commerce以雲端服務和CIF核心元件連接至您的商務系統。 此API對應層通常部署在Adobe I/O Runtime上。 請洽詢您的銷售代表，以取得整合併存取Adobe I/O Runtime。
