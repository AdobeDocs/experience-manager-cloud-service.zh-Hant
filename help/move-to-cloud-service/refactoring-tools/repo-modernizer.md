---
title: Repository Modernizer
description: Repository Modernizer
translation-type: tm+mt
source-git-commit: 5da0d4cc8c6d8781dd7cce8bbbde207568a6d10b
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 3%

---


# Repository Modernizer {#repo-modernizer}

Repository Modernizer是一套公用程式，可將內容和程式碼分隔為獨立的套件，以便與為Adobe Experience Manager定義的專案結構(Cloud Service)相容，借以重組現有的專案套件。

## 簡介 {#introduction}

Adobe Experience Manager即雲端服務，為您的AEM專案帶來許多新功能和可能。 不過，Adobe Experience Manager Maven專案需要進行一些變更，才能與AEM Cloud服務相容。 在高階層，AEM需要將內容和程式碼分 **離為****** 離散子封裝，以尊重可變內容和不可變內容之間的分割。 請參閱 [AEM Project Structure](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) ，以取得有關Cloud Service新AEM專案結構的詳細資訊。

Repository Modernizer會建立下列部署結構，以建立相容的AEM Cloud Service專案結構：

* `ui.apps` 包部署到並包 `/apps` 含所有代碼

* `ui.content` 軟體包部署到運行時可寫區域(如 `/content`、 `/conf`、 `/home`或任何非 `/apps`)，並包含所有內容和設定。

* `all` package是包含子套件和的容器 `ui.apps` 套件 `ui.content`。

>[!NOTE]
>項目結構基於包 *裝及其原型* 24 `pom.xml/filter.xml files`。 如需詳細 [資訊，請參閱](https://github.com/adobe/aem-project-archetype) Archetype 24。

## 使用儲存庫Modernizer {#using-repo-modernizer}

* 通過Adobe I/O CLI :建議您透過 `aio-cli-plugin-aem-cloud-service-migration` （AEM為Adobe I/O CLI的雲端服務程式碼重構外掛程式）使用Repository Modernizer。

   請參閱 **[Git資源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** ，以瞭解如何安裝和使用外掛程式。

* 作為獨立實用程式：Repository Modernizer也可以作為獨立實用程式執行。

   請參閱 **[Git資源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** ，以瞭解如何使用此工具。

   >[!NOTE]
   >
   >Repository Modernizer是使用NodeJS開發的。 建議安裝NodeJS 10.0+。
