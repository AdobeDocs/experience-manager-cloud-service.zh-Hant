---
title: AEM Dispatcher Converter Tool
description: AEM Dispatcher Converter Tool
translation-type: tm+mt
source-git-commit: d3593edcfee660d5ce0b0a8774fe3c61025cbe36
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 12%

---


# AEM Dispatcher Converter {#introduction}

Adobe Experience Manager Dispatcher Converter會將現有的AMS Dispatcher組態轉換為AEM做為Cloud Service Dispatcher組態。

## Dispatcher簡介 {#introduction-dispatcher}

Dispatcher 是 Adobe Experience manager 的快取和/或負載平衡工具。使用 AEM 的 Dispatcher 也有助於保護您的 AEM 伺服器不受攻擊。因此，您可以搭配使用 Dispatcher 與企業級 Web 伺服器，以提高 AEM 例項的安全性。

>[!NOTE]
>The most common use of Dispatcher is to cache responses from an **AEM publish instance**, to increase the responsiveness and security of your externally facing published website.

請參閱 [Dispatcher概述](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) ，瞭解dispatcher如何執行快取、傳回檔案和執行負載平衡。

### Apache和Dispatcher配置和測試 {#dispatcher-configurations-cloud}

您必須瞭解如何將AEM建構為雲端服務Apache和Dispatcher組態，以及如何在部署至雲端環境之前，先在本機驗證並執行它。

如需詳 [細資訊，請參閱Cloud中的](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/dispatcher/overview.html) Dispatcher。

## AEM Dispatcher Converter {#aem-dispatcher-converter}

AEM Dispatcher Converter是一個公用程式，可將現有的AMS Dispatcher組態轉換為AEM做為Cloud Service Dispatcher組態。 此實用程式適用於AMS實例。

所實現的轉換器 **是遵循轉換准則的AEMDispatcherConfigConverter** 。

請參 [閱將AMS轉換為Adobe Experience Manager做為Cloud Service Dispatcher Configuration](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration) ，將AMS轉換為Adobe Experience Manager做為Cloud Service Dispatcher設定。

## 使用AEM Dispatcher Converter {#using-dispatcher-converter}

下節說明使用AEM Dispatcher Converter工具所需的資源和資訊。

請參閱 **[Git資源： AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**，以瞭解此工具的使用、限制和疑難排解。

>[!IMPORTANT]
>AEM Dispatcher Converter是使用Python 3.7.3開發。 建議安裝Python 3.5或更新版本。

## 限制 {#limitations}

AEM Dispatcher Converter的運作假設是，提供的dispatcher設定檔案夾的結構與Cloud Manager dispatcher設定中所述的結構類似。


