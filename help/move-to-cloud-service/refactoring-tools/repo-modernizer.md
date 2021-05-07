---
title: Repository Modernizer
description: Repository Modernizer
exl-id: b89156a8-3d7d-4d36-89a2-beeda35bbc01
translation-type: tm+mt
source-git-commit: 0ed18aad48f33fb0504d59a5f583b5a3dbea59f6
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 4%

---

# 儲存庫Modernizer {#repo-modernizer}

Repository Modernizer是一種實用程式，它通過將內容和代碼分離為離散的包來重組現有項目包，以便與為Adobe Experience Manager定義的項目結構(作為Cloud Service)相容。

## 簡介 {#introduction}

Adobe Experience Manager是Cloud Service，為您的專案帶來許多新功能與可AEM能。 不過，Adobe Experience Manager馬文項目需要進行一些變更，以便與AEMCloud Service相容。 在高級別上，AEM要求將&#x200B;**內容**&#x200B;和&#x200B;**代碼**&#x200B;分離為離散子包，以便遵循可變內容和不可變內容之間的分離。 請參閱[AEM Project Structure](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)以取得有關新項目結構的AEM更多Cloud Service資訊。

Repository Modernizer通過建立以下部AEM署結構建立相容的Cloud Service項目結構：

* `ui.apps` 包部署到並 `/apps` 包含所有代碼

* `ui.content` 包部署到運行時可寫區域(如 `/content`、 `/conf`、 `/home`或任何非 `/apps`)，並包含所有內容和設定。

* `all` package是包含子套件和的容器 `ui.apps` 套件 `ui.content`。

>[!NOTE]
>項目結構基於&#x200B;*包裝的Archetype 24*&#x200B;及其`pom.xml/filter.xml files`。 如需詳細資訊，請參閱[Archetype 24](https://github.com/adobe/aem-project-archetype)。

## 使用Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* 通過Adobe I/OCLI :建議通過`aio-cli-plugin-aem-cloud-service-migration`使用Repository Modernizer(作為Adobe I/OCLI的AEMCloud Service代碼重構插件)。

   請參閱&#x200B;**[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;以瞭解如何安裝和使用外掛程式。

* 作為獨立實用程式：Repository Modernizer也可以作為獨立實用程式執行。

   請參閱&#x200B;**[Git資源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)**&#x200B;以瞭解如何使用此工具。

   >[!NOTE]
   >
   >Repository Modernizer是使用NodeJS開發的。 建議安裝NodeJS 10.0+。
