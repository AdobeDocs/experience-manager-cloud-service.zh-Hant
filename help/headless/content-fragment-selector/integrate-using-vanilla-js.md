---
title: 使用Vanilla JS整合內容片段選擇器
description: 整合內容片段選擇器與各種Adobe、非Adobe和第三方應用程式。
role: Admin, User, Developer
source-git-commit: 592e443928f2c9c18ac281027026132b1c877ce3
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---

# 使用Vanilla JS整合內容片段選擇器 {#integrate-content-fragment-selector-using-vanilla-js}

您可以將任何Adobe或非Adobe應用程式與Adobe Experience Manager (AEM) as a Cloud存放庫整合，並從該應用程式中選取內容片段。

整合是透過匯入內容片段選擇器套件並使用Vanilla JavaScript程式庫連線至AEM as a Cloud Service來完成。 編輯`index.html`或您應用程式內的任何適當檔案，以：

* 定義身份驗證詳細資訊
* 存取AEM as a Cloud Service存放庫
* 設定內容片段選擇器的顯示屬性

如果您符合下列條件，則您可以在不定義某些IMS屬性的情況下執行驗證：

* 正在[Unified Shell](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/overview/aem-cloud-service-on-unified-shell)上整合Adobe應用程式
* 已產生用於驗證的IMS權杖
