---
title: Repository Modernizer
description: Repository Modernizer
source-git-commit: a6d225943c5d23ebd960fda0b0912a81f1f80014
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# Repository Modernizer {#repo-modernizer}

Repository Modernizer是一項公用程式，旨在將內容和程式碼分割為獨立套件，以與Adobe Experience Manager as a Cloud Service所定義的專案結構相容，借此重新建構現有的專案套件。

## 簡介 {#introduction}

Adobe Experience Manager as a Cloud Service為您的AEM專案帶來許多新功能，並帶來許多可能性。 不過，Adobe Experience Manager Maven專案需進行一些變更，才能與AEM Cloud Service相容。 在高階層，AEM需要 **內容** 和 **代碼** 分離子包，以遵循可變內容和不可變內容之間的分割。 請參閱 [AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 如需新AEM專案結構的詳細資訊，請Cloud Service。

Repository Modernizer會建立下列部署結構，以建立相容的AEM Cloud Service專案結構：

* `ui.apps` 包部署 `/apps` 並包含所有程式碼

* `ui.content` 包部署到運行時可寫區域(例如 `/content`, `/conf`, `/home`或其他 `/apps`)和包含所有內容和設定。

* `all` 包是包含子包的容器包 `ui.apps` 和 `ui.content`.

>[!NOTE]
>專案結構以 *原型24* 包及其 `pom.xml/filter.xml files`. 請參閱 [原型24](https://github.com/adobe/aem-project-archetype) 以取得更多詳細資訊。

## 使用Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* 通過Adobe I/OCLI :建議您透過 `aio-cli-plugin-aem-cloud-service-migration` (AEMas a Cloud Service程式碼重構Adobe I/OCLI的外掛程式)。

   請參閱 **[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 了解如何安裝及使用外掛程式。

* 作為獨立公用程式：Repository Modernizer也可作為獨立公用程式執行。

   請參閱 **[Git資源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** 了解如何使用此工具。

   >[!NOTE]
   >
   >Repository Modernizer是使用NodeJS開發。 建議安裝NodeJS 10.0+。
