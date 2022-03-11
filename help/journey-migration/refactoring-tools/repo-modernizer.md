---
title: 儲存庫現代化器
description: 儲存庫現代化器
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 4%

---

# 儲存庫現代化器 {#repo-modernizer}

Repository Modernizer是一種實用程式，它通過將內容和代碼分離為離散的包以與為Adobe Experience Manager as a Cloud Service定義的項目結構相容，從而重構現有項目包。

## 簡介 {#introduction}

Adobe Experience Manager as a Cloud Service為你的項目帶來了許多新特AEM點和可能性 但是，Adobe Experience Manager馬文項目需要一些變化，以與AEM Cloud Service相容。 在高級別上，AEM需要將 **內容** 和 **代碼** 分為離散子包，以考慮可變內容和不可變內容之間的分割。 請參閱 [項AEM目結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 的子菜單。

儲存庫現代化器通過建立以下部署結構建立相容的AEM Cloud Service項目結構：

* `ui.apps` 包部署到 `/apps` 包含所有代碼

* `ui.content` 包部署到運行時可寫區域(例如 `/content`。 `/conf`。 `/home`，或者 `/apps`包含所有內容和配置。

* `all` 包是包含子包的容器包 `ui.apps` 和 `ui.content`。

>[!NOTE]
>項目結構基於 *原型24* 包和包 `pom.xml/filter.xml files`。 請參閱 [原型24](https://github.com/adobe/aem-project-archetype) 的子菜單。

## 使用儲存庫現代化器 {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* 通過Adobe I/OCLI :建議通過以下方式使用「儲存庫現代化器」 `aio-cli-plugin-aem-cloud-service-migration` (AEMAdobe I/OCLI的as a Cloud Service代碼重構插件)。

   請參閱 **[Git資源：aio-cli-plugin-aem — 雲服務 — 遷移](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 瞭解如何安裝和使用插件。

* 作為獨立實用程式：也可以將Repository Modernizer作為獨立實用程式執行。

   請參閱 **[Git資源：儲存庫現代化器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** 瞭解如何使用此工具。

   >[!NOTE]
   >
   >儲存庫現代化器是使用NodeJS開發的。 建議安裝NodeJS 10.0+。
