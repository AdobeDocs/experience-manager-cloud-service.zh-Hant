---
title: HTML5表單快速入門
description: 若要開始使用，請部署AEM Forms附加元件套件，並將現有的HTML5表單匯入至AEM。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f276d150-8936-4bfb-8475-7ca36815b233
feature: HTML5 Forms,Mobile Forms
exl-id: a3245f05-6ea3-4f90-8981-bfa89d2e7335
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# HTML5表單快速入門 {#getting-started-with-html-forms}

<span class="preview"> HTML5 Forms功能屬於Early Access方案的一部分。 若要要求存取權，請將您的正式（工作）電子郵件ID傳送電子郵件至aem-forms-ea@adobe.com。
</span>

HTML5表單提供多項適用於行動裝置的功能。 它可協助您將目前的解決方案和工作流程擴展至使用HTML5瀏覽器的平板電腦或智慧型手機裝置。 部分功能包括：

* **以HTML5轉譯XFA表單範本：**&#x200B;除了一般PDF forms之外，您現在也可以以HTML5格式轉譯現有的XFA表單。 這可協助您將使用者端平台擴充至支援HTML5且使用XFA Forms不支援Adobe Reader的行動裝置(Apple iPad、Android平板電腦、智慧型手機等)。 如需HTML5轉譯功能的詳細資訊，請參閱[HTML5表單簡介](/help/forms/introductionhtml5.md)。

* **管理Forms：**&#x200B;此外，AEM還包含可簡化組織和管理表單流程的新功能。 您可以啟用、停用、發佈及預覽表單。<!--For more information, see [Introduction to managing forms](/help/forms/using/introduction-managing-forms.md).-->

## 為HTML5表單設定環境 {#installing-html-forms}

若要啟用表單提交和正確轉譯HTML5 Forms，請執行以下步驟：

* **新增Dispatcher篩選器：**&#x200B;更新您的`src/conf.dispatcher.d/filters/filters.any`檔案，以允許HTML5 Forms的必要請求。 新增下列篩選規則：

  ```
  /0103 { /type "allow" /method '(HEAD|POST)' /url "/content/xfaforms/profiles/default.submit.html" }  # allow POSTs to form selectors under content
  /0104 { /type "allow" /method '(GET|HEAD|POST)' /url "/*.xdp.html" }
  ```

* **新增要提交的封裝：**&#x200B;在您的專案中，在`src/main/content/jcr_root/content`資料夾中新增封裝，以支援表單提交功能。

* **匯入HTML5 Forms：**&#x200B;將表單從您的本機檔案系統匯入至AEM Forms。
