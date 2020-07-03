---
title: AEM Dispatcher 轉換工具
description: AEM Dispatcher 轉換工具
translation-type: tm+mt
source-git-commit: 66cf4fc7b5a336968dd3f8757cc56a11d6e4843e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 94%

---


# AEM Dispatcher 轉換工具 {#introduction}

「Adobe Experience Manager Dispatcher 轉換工具」會將現有的 AMS Dispatcher 設定轉換為 AEM 雲端服務設定。

## Dispatcher 簡介 {#introduction-dispatcher}

Dispatcher 是 Adobe Experience manager 的快取和/或負載平衡工具。使用 AEM 的 Dispatcher 也有助於保護您的 AEM 伺服器不受攻擊。因此，您可以搭配使用 Dispatcher 與企業級 Web 伺服器，以提高 AEM 例項的安全性。

>[!NOTE]
>Dispatcher 最常見的用法是快取來自 **AEM Publish 例項**&#x200B;的回應，以提高您對外發佈網站的回應速度與安全性。

請參考 [Dispatcher 綜覽](https://docs.adobe.com/content/help/zh-Hant/experience-manager-dispatcher/using/dispatcher.html)，了解 Dispatcher 如何執行快取、傳回文件和執行負載平衡。

### Apache 和 Dispatcher 設定和測試 {#dispatcher-configurations-cloud}

您必須了解如何構成 AEM 雲端服務 Apache 和 Dispatcher 設定，以及如何在部署至雲端環境前，先在本機上驗證並執行。

如需詳細資訊，請參考[雲端上的 Dispatcher](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html)。

## AEM Dispatcher 轉換工具 {#aem-dispatcher-converter}

AEM Dispatcher 轉換工具是一個公用程式，可將現有的 AMS Dispatcher 設定轉換為 AEM 雲端服務設定。此公用程式適用於 AMS 例項。

實作的轉換工具為遵循轉換准則的 **AEMDispatcherConfigConverter**。

如果要將 AMS 轉換為 Adobe Experience Manager 雲端服務 Dispatcher 設定，請參考[將 AMS 轉換為 Adobe Experience Manager 雲端服務 Dispatcher 設定](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/content-delivery/disp-overview.html#how-to-convert-an-ams-to-an-aem-as-a-cloud-service-dispatcher-configuration)。

## 使用 AEM Dispatcher 轉換工具 {#using-dispatcher-converter}

以下章節說明使用「AEM Dispatcher 轉換工具」所需的資源和資訊。

請參考 **[Git 資源：AEM 雲端服務 Dispatcher 轉換工具](https://github.com/adobe/aem-cloud-service-dispatcher-converter)**，了解此工具的使用方式、限制和疑難排解資訊。

>[!IMPORTANT]
>AEM Dispatcher 轉換工具使用 Python 3.7.3 開發。建議安裝 Python 3.5 或更新的版本。

## 限制 {#limitations}

「AEM Dispatcher 轉換工具」根據以下假設運作：所提供的 Dispatcher 設定資料夾的結構，類似於 Cloud Manager Dispatcher 設定中描述的結構。


