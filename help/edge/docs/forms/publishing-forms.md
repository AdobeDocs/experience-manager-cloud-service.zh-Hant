---
title: 發佈Forms for Edge Delivery Services
description: 瞭解表單發佈如何與Edge Delivery Services搭配使用，以及如何使用Edge Delivery Services發佈AEM表單。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---


# 發佈Forms for Edge Delivery Services

本文會引導您完成將表單發佈至AEMEdge Delivery Services的程式。
若要將表單發佈至Edge Delivery Services，您必須先建立AEM環境與GitHub存放庫之間的連線。 連線後，您可以使用通用編輯器編寫表單，其會遵循WYSIWYG (What You See Is What You Get)方法，提供順暢且一致的Sites使用者體驗。

## 必要條件

* 剛開始使用最適化Forms？ 依照提供的[教學課程](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)設定您的GitHub存放庫。
* 如果您已在使用Edge Delivery Services，請將最新版本的[最適化Forms區塊](/help/edge/docs/forms/tutorial.md#)新增至您的GitHub存放庫。
* AEM Forms製作例項包含以Edge Delivery Services為基礎的範本。 請確定您的環境中已安裝[最新版本的核心元件](https://github.com/adobe/aem-core-forms-components)。
* 讓您的AEM Formsas a Cloud Service編寫執行個體和GitHub存放庫的URL隨時待命。

## 適用於Edge Delivery Services的Publish Forms

若要發佈Edge Delivery Services表單，請執行以下步驟：

[1.將GitHub存放庫連結至AEM執行個體](#link-github-repository-to-aem-instance)

[2.將AEM執行個體連結至GitHub存放庫](#link-aem-instance-to-github-repository)

### 將GitHub存放庫連結至AEM執行個體

若要將GitHub存放庫](/help/edge/docs/forms/tutorial.md)上的[專案連結至AEM Forms Author執行個體，請執行下列步驟：

1. 前往您為Edge Delivery Services建立或設定的GitHub存放庫。
1. 開啟 `fstab.yaml` 檔案進行編輯。
1. 以您AEM Formsas a Cloud Service執行個體的URL更新您GitHub存放庫中的`fstab.yaml`檔案。

   ```javascript
    mountpoints:
    /:
        url: [author-instance-url]/bin/franklin.delivery/[Github owner]/[Github Repository]/[Github branch] 
        type: "markup"
        suffix: ".html"
   ```

   例如，如果您的GitHub存放庫名為「aemcrossswalk」，位於帳戶「wkndform」下方，而您使用的是「主要」分支，則作者執行個體URL看起來會像這樣：

   ```
        mountpoints:
            /:
            url: https://author-p133911-e1313554.adobeaemcloud.com/bin/franklin.delivery/wkndform/aemcrosswalk/main
            type: "markup"
            suffix: ".html"
   ```

1. 認可對`fstab.yaml`檔案的變更。

### 將AEM執行個體連結至GitHub存放庫

若要將AEM Forms Author執行個體連結至[您在GitHub存放庫上的專案](/help/edge/docs/forms/tutorial.md)，請執行下列步驟：

[1.根據Edge Delivery Services範本建立最適化表單](#1-create-an-adaptive-form-based-on-the-edge-delivery-services-template)

[2.在AEM編寫執行個體中找到您的表單設定容器](#2-locate-your-forms-configuration-container-in-aem-author-instance)

[3.在通用編輯器中編寫表單](#3-author-the-form-in-the-universal-editor)

[4. Publish並預覽表單](#4-publish-and-preview-the-form)

#### 1.根據Edge Delivery Services範本建立最適化表單

1. 存取您的AEM Formsas a Cloud Service編寫執行個體。
1. 選取&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。1.選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 最適化Forms]**。 此時會開啟精靈。在Source標籤中，選取以Edge Delivery Services為基礎的formtemplate：

   ![建立EDS Forms](/help/edge/assets/create-eds-forms.png){width=50%， align-center}

1. 按一下「**[!UICONTROL 建立]**」，就會顯示「**建立表單**」精靈。
1. 指定&#x200B;**GitHub URL**。 舉例來說，如果您的GitHub存放庫名為「aemcrossswalk」，且位於帳戶「wkndform」下方，則URL會是：
   `https://github.com/wkndform/aemcrosswalk`
1. 按一下&#x200B;**[!UICONTROL 建立]**。

   ![建立表單精靈](/help/edge/assets/create-form-wizard.png){width=50%， align-center}

   按一下&#x200B;**[!UICONTROL 建立]**&#x200B;後，表單就會在Universal編輯器中開啟以進行編寫。

   ![編寫表單](/help/edge/assets/author-form.png){width=50%， align-center}

   >[!NOTE]
   >
   > Edge Delivery Services系統會根據表單的設定容器自動建立表單的Edge Delivery Services設定。

#### 2.在AEM編寫執行個體中找到您的表單設定容器

1. 導覽至您AEM Formsas a Cloud Service作者執行個體上的&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL Edge Delivery Services設定]**。
1. 選取符合表單名稱的資料夾。 例如，如果您的表單名為&#39;contact-us&#39;，請選擇資料夾`forms/contact-us`並選取設定併發佈設定：

   ![Edge Delivery Services組態](/help/forms/assets/aem-instance-eds-configuration.png){width=50%， align-center}

1. 按一下&#x200B;**[!UICONTROL 屬性]**&#x200B;檢視組態。\
   ![自動建立的組態](/help/edge/assets/aem-forms-create-configuration-github.png){width=50%， align-center}

   Edge主機選項維持原狀。 表單會發佈到預覽(.page)和即時(.live)環境。

1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**。設定已儲存。

#### 3.在通用編輯器中編寫表單

當您按一下&#x200B;**[!UICONTROL 建立]**&#x200B;時，表單會在Universal Editor中開啟以進行編寫。

1. 開啟內容瀏覽器，並導覽至&#x200B;**內容樹狀結構**&#x200B;中的&#x200B;**[!UICONTROL 最適化表單]**&#x200B;元件。

   ![內容樹狀結構](/help/edge/assets/content-tree.png){width=50%， align-center}

1. 按一下「**[!UICONTROL 新增]**」圖示，並從「**最適化表單元件**」清單新增所需的元件。

   ![新增元件](/help/edge/assets/add-component.png){width=50%， align-center}

1. 選取新增的最適化表單元件，並使用&#x200B;**[!UICONTROL 屬性]**&#x200B;更新其屬性。

   ![開啟屬性](/help/edge/assets/component-properties.png){width=50%， align-center}

   下面的熒幕擷圖顯示了在通用編輯器中編寫的簡單「聯絡我們」表單：

   ![與我們連絡表單](/help/edge/assets/contact-us.png){width=50%， align-center}

#### 4. Publish並預覽表單

現在，按一下Universal Editor右上角的&#x200B;**[!UICONTROL Publish]**&#x200B;按鈕，將表單發佈到Edge Delivery Services。

![發佈表單](/help/edge/assets/publish-form.png){width=50%， align-center}


以下說明如何存取Edge Delivery Services上的表單：

* **階段版本（用於測試）**：階段版本顯示表單的未發佈、運作中版本以用於測試目的。 在表單上線之前，請使用下列URL格式來預覽表單：

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  例如，如果專案的存放庫命名為「aemcrossswalk」，位於帳戶「wkndform」下方，而您使用「主要」分支和表單作為「聯絡我們」，則分段版本URL如下所示：
https://main--aemcrosswalk--wkndform.aem.page/content/forms/af/contact-us

* **即時版本（已發佈的表單）**：   即時版本會顯示最新發佈的表單版本，以供一般使用者存取。 使用下列URL格式存取已發佈的即時表單版本：

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  例如，如果專案的存放庫命名為「aemcrossswalk」，位於帳戶「wkndform」下方，而您使用「主要」分支和表單作為「聯絡我們」，則分段版本URL如下所示：
https://main--aemcrosswalk--wkndform.aem.live/content/forms/af/contact-us

各階段版本和即時版本的URL結構都維持相同。 不過，您看到的內容會因內容而異：

![檢視已發佈的表單](/help/edge/assets/eds-view-publish-form.png){width=50%， align-center}

## 疑難排解

載入表單時發生問題？ 以下是一些常見問題以及如何加以修正：

* **表單URL**：仔細檢查表單URL的結尾是否不包含「.html」副檔名。 Edge Deliver Service不需要此擴充功能。

* **AEM作者URL** L：請確定`fstab.yaml`檔案中所列的AEM作者URL格式正確。 其中應包括下列詳細資訊：

   * 正確的GitHub擁有者
   * 正確的存放庫名稱
   * 您用於Edge Delivery Services的特定分支

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## 另請參閱

{{see-more-forms-eds}}