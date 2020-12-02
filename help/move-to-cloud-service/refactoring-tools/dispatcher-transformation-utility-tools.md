---
title: AEM Dispatcher 轉換工具
description: AEM Dispatcher 轉換工具
translation-type: tm+mt
source-git-commit: 50d26dbec8281afec07ca56595b4b2a7b915eca9
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 53%

---


# AEM Dispatcher 轉換工具 {#introduction}

Adobe Experience Manager Dispatcher Converter會將現有的AEM Dispatcher組態轉換為AEM，做為Cloud Service Dispatcher組態。

## Dispatcher 簡介 {#introduction-dispatcher}

Dispatcher 是 Adobe Experience manager 的快取和/或負載平衡工具。使用 AEM 的 Dispatcher 也有助於保護您的 AEM 伺服器不受攻擊。因此，您可以搭配使用 Dispatcher 與企業級 Web 伺服器，以提高 AEM 例項的安全性。

>[!NOTE]
>Dispatcher 最常見的用法是快取來自 **AEM Publish 例項**&#x200B;的回應，以提高您對外發佈網站的回應速度與安全性。

請參考 [Dispatcher 綜覽](https://docs.adobe.com/content/help/zh-Hant/experience-manager-dispatcher/using/dispatcher.html)，了解 Dispatcher 如何執行快取、傳回文件和執行負載平衡。

### Apache 和 Dispatcher 設定和測試 {#dispatcher-configurations-cloud}

您必須了解如何構成 AEM as a Cloud Service Apache 和 Dispatcher 設定，以及如何在部署至雲端環境前，先在本機上驗證並執行。

如需詳細資訊，請參考[雲端上的 Dispatcher](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html)。

## AEM Dispatcher 轉換工具 {#aem-dispatcher-converter}

AEM Dispatcher Converter提供將現有內部部署或Adobe Managed Services Dispatcher組態重構為AEM的功能，做為Cloud Service相容的Dispatcher組態。

## 使用 AEM Dispatcher 轉換工具 {#using-dispatcher-converter}

* 通過Adobe I/O CLI :建議您透過`aio-cli-plugin-aem-cloud-service-migration`使用AEM Dispatcher Converter（AEM為Adobe I/O CLI的雲端服務程式碼重構外掛程式）。

   請參閱&#x200B;**[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;以瞭解如何安裝和使用外掛程式。

* 作為獨立實用程式：AEM Dispatcher Converter工具也可以當成獨立的公用程式執行。

   請參閱&#x200B;**[Git資源：AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)**，以瞭解此工具的使用與疑難排解。

>[!IMPORTANT]
>AEM Dispatcher Converter是使用NodeJS開發。 建議安裝NodeJS 10.0+。

