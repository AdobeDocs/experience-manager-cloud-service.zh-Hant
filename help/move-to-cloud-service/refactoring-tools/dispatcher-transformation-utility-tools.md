---
title: AEM Dispatcher 轉換工具
description: AEM Dispatcher 轉換工具
exl-id: 97eb4f3f-dc03-461a-8d7e-164065bd1e4c
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 48%

---

# AEM Dispatcher 轉換工具 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher 轉換工具"
>abstract="Adobe Experience Manager Dispatcher轉換工具會將現有的AEM Dispatcher設定轉換為AEM做為Cloud ServiceDispatcher設定。"

Adobe Experience Manager Dispatcher轉換工具會將現有的AEM Dispatcher設定轉換為AEM做為Cloud ServiceDispatcher設定。

## Dispatcher 簡介 {#introduction-dispatcher}

Dispatcher 是 Adobe Experience manager 的快取和/或負載平衡工具。使用 AEM 的 Dispatcher 也有助於保護您的 AEM 伺服器不受攻擊。因此，您可以搭配使用 Dispatcher 與企業級 Web 伺服器，以提高 AEM 例項的安全性。

>[!NOTE]
>Dispatcher 最常見的用法是快取來自 **AEM Publish 例項**&#x200B;的回應，以提高您對外發佈網站的回應速度與安全性。

請參考 [Dispatcher 綜覽](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant)，了解 Dispatcher 如何執行快取、傳回文件和執行負載平衡。

### Apache 和 Dispatcher 設定和測試 {#dispatcher-configurations-cloud}

您必須了解如何構成 AEM as a Cloud Service Apache 和 Dispatcher 設定，以及如何在部署至雲端環境前，先在本機上驗證並執行。

如需詳細資訊，請參考[雲端上的 Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html)。

## AEM Dispatcher 轉換工具 {#aem-dispatcher-converter}

AEM Dispatcher Converter可重構現有的內部部署或Adobe Managed Services Dispatcher設定，做為與AEM相容的Cloud ServiceDispatcher設定。

## 使用 AEM Dispatcher 轉換工具 {#using-dispatcher-converter}

* 通過Adobe I/OCLI :建議您透過`aio-cli-plugin-aem-cloud-service-migration`使用AEM Dispatcher轉換工具(AEM作為Adobe I/OCLI的Cloud Service程式碼重構外掛程式)。

   請參閱&#x200B;**[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;以了解如何安裝及使用外掛程式。

* 作為獨立公用程式：AEM Dispatcher轉換工具也可以作為獨立公用程式執行。

   請參閱&#x200B;**[Git資源：AEMCloud ServiceDispatcher轉換工具](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)**&#x200B;以了解此工具的使用方式和疑難排解。

>[!IMPORTANT]
>AEM Dispatcher轉換工具是使用NodeJS開發。 建議安裝NodeJS 10.0+。
