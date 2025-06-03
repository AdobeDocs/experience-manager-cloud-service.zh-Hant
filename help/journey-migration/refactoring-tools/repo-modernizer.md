---
title: 存放庫現代化工具
description: 瞭解如何重新建構現有的專案套件，使其與針對Adobe Experience Manager as a Cloud Service定義的專案結構相容。
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
feature: Migration
role: Admin
source-git-commit: 6920651420da9b427510518b7add0637479adef5
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 2%

---

# 存放庫現代化工具 {#repo-modernizer}

Repository Modernizer是專為重組現有專案套件而開發的公用程式，其將內容和程式碼分割為獨立套件，以與Adobe Experience Manager as a Cloud Service定義的專案結構相容。

## 簡介 {#introduction}

Adobe Experience Manager as a Cloud Service為您的AEM專案提供許多新功能和可能性。 不過，Adobe Experience Manager Maven專案必須進行一些變更，才能與AEM雲端服務相容。 在高層面上，AEM需要將&#x200B;**內容**&#x200B;和&#x200B;**程式碼**&#x200B;分離為離散的子套件，以遵循可變和不可變內容之間的分割。 請參閱[AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html)，以取得Cloud Service新AEM專案結構的詳細資訊。

Repository Modernizer會建立下列部署結構，以建立相容的AEM Cloud Service專案結構：

* `ui.apps`套件部署至`/apps`並包含所有程式碼

* `ui.content`套件部署到執行階段可寫入的區域（例如，`/content`、`/conf`、`/home`或非`/apps`的任何專案）並包含所有內容和設定。

* `all`封裝是包含子封裝`ui.apps`和`ui.content`的容器封裝。

>[!NOTE]
>
>專案結構是以封裝及其`pom.xml/filter.xml files`的&#x200B;*原型24*&#x200B;為基礎。 如需詳細資訊，請參閱[原型24](https://github.com/adobe/aem-project-archetype)。

## 使用Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* 透過Adobe I/O CLI ：Adobe建議透過`aio-cli-plugin-aem-cloud-service-migration` (Adobe I/O CLI的AEM as a Cloud Service程式碼重構外掛程式)使用Repository Modernizer。

  請參閱&#x200B;**[Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**，瞭解如何安裝及使用外掛程式。

* 作為獨立公用程式： Repository Modernizer也可以作為獨立公用程式執行。

  請參閱&#x200B;**[Git資源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)**，以瞭解如何使用此工具。

  >[!NOTE]
  >
  >Repository Modernizer是使用NodeJS開發。 建議安裝NodeJS 10.0+。
