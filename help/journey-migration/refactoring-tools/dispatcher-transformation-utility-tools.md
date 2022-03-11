---
title: AEM Dispatcher 轉換工具
description: AEM Dispatcher 轉換工具
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 48%

---

# AEM Dispatcher 轉換工具 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher 轉換工具"
>abstract="Adobe Experience ManagerDispatcher Converter將現有AEMDispatcher配置轉換為AEMas a Cloud Service的Dispatcher配置。"

Adobe Experience ManagerDispatcher Converter將現有AEMDispatcher配置轉換為AEMas a Cloud Service的Dispatcher配置。

## Dispatcher 簡介 {#introduction-dispatcher}

Dispatcher 是 Adobe Experience manager 的快取和/或負載平衡工具。使用 AEM 的 Dispatcher 也有助於保護您的 AEM 伺服器不受攻擊。因此，您可以搭配使用 Dispatcher 與企業級 Web 伺服器，以提高 AEM 例項的安全性。

>[!NOTE]
>Dispatcher 最常見的用法是快取來自 **AEM Publish 例項**&#x200B;的回應，以提高您對外發佈網站的回應速度與安全性。

請參考 [Dispatcher 綜覽](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant)，了解 Dispatcher 如何執行快取、傳回文件和執行負載平衡。

### Apache 和 Dispatcher 設定和測試 {#dispatcher-configurations-cloud}

您必須了解如何構成 AEM as a Cloud Service Apache 和 Dispatcher 設定，以及如何在部署至雲端環境前，先在本機上驗證並執行。

如需詳細資訊，請參考[雲端上的 Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html)。

## AEM Dispatcher 轉換工具 {#aem-dispatcher-converter}

AEM Dispatcher Converter提供了將現有的本地或Adobe Managed Services Dispatcher配置重構為as a Cloud Service相容的AEMDispatcher配置的功能。

## 使用 AEM Dispatcher 轉換工具 {#using-dispatcher-converter}

* 通過Adobe I/OCLI :建議使用Dispatcher Converter(AEMDispatcher Converter) `aio-cli-plugin-aem-cloud-service-migration` (AEMAdobe I/OCLI的as a Cloud Service代碼重構插件)。

   請參閱 **[Git資源：aio-cli-plugin-aem — 雲服務 — 遷移](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 瞭解如何安裝和使用插件。

* 作為獨立實用程式：Dispatcher Converter工AEM具也可以作為獨立實用程式執行。

   請參閱 **[Git資源：AEM Cloud Service調度器轉換器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** 瞭解此工具的用法和故障排除。

>[!IMPORTANT]
>Dispatcher ConverterAEM是使用NodeJS開發的。 建議安裝NodeJS 10.0+。
