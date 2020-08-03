---
title: AEM Commerce as a Cloud Service快速入門
description: AEM Commerce as a Cloud Service快速入門
translation-type: tm+mt
source-git-commit: 170a6f4f3aa07b9aa917014b7a682ead9ed595c1
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 2%

---


# AEM Commerce as a Cloud Service快速入門 {#start}

若要以雲端服務的形式開始使用AEM Commerce，您的Experience Manager Cloud服務必須配備Commerce Integration Framework(CIF)附加元件。 CIF附加元件是 [AEM Sites（雲端服務）之上的額外模組](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/sites/home.html)。

## 入門 {#onboarding}

AEM Commerce即雲端服務的上線程式是兩個步驟：

1. 啟用AEM Commerce即雲端服務，並布建CIF附加元件
2. 將AEM Commerce以雲端服務方式與您的Magento環境連接

第一步由Adobe完成。 您需要提供IMS組織、GraphQL端點URL等資訊。 作為布建過程的一部分。 如需定價和布建的詳細資訊，您必須聯絡銷售代表。

一旦您獲得CIF附加元件的布建，該附加元件將應用於任何現有的Cloud Manager程式。 如果您沒有Cloud Manager計畫，則需要建立新計畫。 有關詳細資訊，請參閱 [設定程式](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/setting-up-program.html)。

第二個步驟是針對每個AEM提供自助服務，做為雲端服務環境。 在CIF附加元件初始布建後，您還需要進行一些其它配置。

## 將AEM Commerce與Magento連接 {#magento}

若要將CIF附加元件和 [AEM CIF核心元件與您的Magento環境連接](https://github.com/adobe/aem-core-cif-components) ，您需要透過Cloud Manager環境變數提供Magento GraphQL端點URL。 變數名稱為 `COMMERCE_ENDPOINT`。 必須配置通過HTTPS的安全連接。
每個AEM都可以使用不同的Magento GraphQL端點URL做為雲端服務環境。 如此，專案就可將AEM測試環境與Magento測試系統和AEM生產環境連接至Magento生產系統。 Magento GraphQL端點必須是公開可用的，不支援專用VPN或本地連接。

若要將AEM Commerce與Magento連線，請依照下列步驟進行：

1. 使用Cloud Manager增效模組取得Adobe I/O CLI

   請查看 [Adobe Cloud Manager檔案](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html) ，瞭解如何下載、設定和使用 [Adobe I/O CLI與](https://github.com/adobe/aio-cli) Cloud Manager CLI外掛程式 [](https://github.com/adobe/aio-cli-plugin-cloudmanager)。

2. 以AEM作為雲端服務程式驗證CLI

3. 在Cloud Manager `COMMERCE_ENDPOINT` 中設定變數

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   如需詳 [細資訊](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) ，請參閱CLI檔案。

   Magento GraphQL端點URL必須指向Magento的GraphQl服務，並使用安全的HTTPS連接。 For example: `https://demo.magentosite.cloud/graphql`.

>[!TIP]
>
>您可以使用下列命令列出所有Cloud Manager變數以進行複查： `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

>[!Note]
>
>您也可以使 [用Cloud Manager API](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html) ，來設定Cloud Manager變數。

有了這項功能，您就可以將AEM Commerce當做雲端服務使用，而且可以透過Cloud Manager部署專案。

## 第三方商務整合 {#integrations}

對於協力廠商商務整合，需要 [API對應層](architecture/third-party.md) ，才能將AEM Commerce以雲端服務和CIF核心元件的形式與您的商務系統連接。 此API對應層通常部署在Adobe I/O Runtime上。 請洽詢您的銷售代表，以取得整合併存取Adobe I/O Runtime。
