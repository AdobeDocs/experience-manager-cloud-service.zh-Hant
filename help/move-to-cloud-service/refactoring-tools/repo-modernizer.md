---
title: Repository Modernizer
description: Repository Modernizer
exl-id: b89156a8-3d7d-4d36-89a2-beeda35bbc01
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# Repository Modernizer {#repo-modernizer}

Repository Modernizer是一項公用程式，旨在將內容和程式碼分割為獨立套件，以與Adobe Experience Manager(Resopitory)所定義的Cloud Service結構相容，借此重新建構現有的專案套件。

## 簡介 {#introduction}

Adobe Experience Manager as aCloud Service為您的AEM專案帶來許多新功能，並帶來許多可能性。 不過，Adobe Experience Manager Maven專案需進行一些變更，才能與AEMCloud Service相容。 在高級別上，AEM要求將&#x200B;**content**&#x200B;和&#x200B;**code**&#x200B;分離為離散子包，以遵循可變內容和不可變內容之間的分割。 有關新AEM專案結構以進行Cloud Service的詳細資訊，請參閱[AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)。

Repository Modernizer會建立下列部署結構，以建立相容的AEMCloud Service專案結構：

* `ui.apps` 套件部署至並 `/apps` 包含所有程式碼

* `ui.content` 包部署到運行時可寫區域(例如 `/content`、  `/conf`、  `/home`或任何非 `/apps`)，並包含所有內容和設定。

* `all` 包是包含子包和的容器 `ui.apps` 包 `ui.content`。

>[!NOTE]
>專案結構是以套件及其`pom.xml/filter.xml files`的原型24 *為基礎。*&#x200B;如需詳細資訊，請參閱[原型24](https://github.com/adobe/aem-project-archetype)。

## 使用Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* 通過Adobe I/OCLI :建議您透過`aio-cli-plugin-aem-cloud-service-migration`使用Repository Modernizer(AEM為Adobe I/OCLI的Cloud Service程式碼重構外掛程式)。

   請參閱&#x200B;**[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;以了解如何安裝及使用外掛程式。

* 作為獨立公用程式：Repository Modernizer也可作為獨立公用程式執行。

   請參閱&#x200B;**[Git資源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)**&#x200B;了解如何使用此工具。

   >[!NOTE]
   >
   >Repository Modernizer是使用NodeJS開發。 建議安裝NodeJS 10.0+。
