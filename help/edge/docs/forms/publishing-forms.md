---
title: 為 Edge Delivery Services 發佈表單
description: 了解表單發佈如何與 Edge Delivery Services 搭配使用，以及如何使用 Edge Delivery Services 發佈 AEM 表單。
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: b90c27e3-22ea-4b18-b16e-a5c5a0ed58b8
source-git-commit: 67384a9141ced3bf5be63c8489dd5c329a288056
workflow-type: ht
source-wordcount: '993'
ht-degree: 100%

---

# 為 Edge Delivery Services 發佈表單

本文會引導您完成將表單發佈到 AEM Edge Delivery Services 的流程。
若要將表單發佈到 Edge Delivery Services，您必須先在 AEM 環境和 GitHub 存放庫之間建立連線。連線後，您即可使用通用編輯器製作表單，該編輯器會依照 WYSIWYG (所見即所得) 方法為 Sites 提供無縫且一致的使用者體驗。

## 必要條件

* 第一次使用最適化表單？請依照所提供的[教學課程](/help/edge/docs/forms/tutorial.md#add-adaptive-forms-block-to-your-existing-aem-project)設定 GitHub 存放庫。
* 如果您已使用 Edge Delivery Services，請將最新版本的[最適化表單區塊](/help/edge/docs/forms/tutorial.md#)新增至您的 GitHub 存放庫。
* AEM 表單作者執行個體包括根據 Edge Delivery Services 建立的範本。請確保您的環境中安裝了[最新版本的核心元件](https://github.com/adobe/aem-core-forms-components)。
* 將 AEM Forms 作為雲端服務作者執行個體的 URL 和 GitHub 存放庫保持便於使用。

## 為 Edge Delivery Services 發佈表單

若要為 Edge Delivery Services 發佈表單，請執行下列步驟：

[1. 將 GitHub 存放庫連結到 AEM 執行個體](#link-github-repository-to-aem-instance)

[2. 將 AEM 執行個體連結到 GitHub 存放庫](#link-aem-instance-to-github-repository)

### 將 GitHub 存放庫連結到 AEM 執行個體

若要將[您在 GitHub 存放庫上的專案](/help/edge/docs/forms/tutorial.md)連結到 AEM Forms 作者執行個體，請執行下列步驟：

1. 請前往您為 Edge Delivery Services 建立或設定的 GitHub 存放庫。
1. 開啟 `fstab.yaml` 檔案進行編輯。
1. 使用 AEM Forms 作為雲端服務執行個體的 URL 來更新 GitHub 存放庫中的 `fstab.yaml` 檔案。

   ```javascript
    mountpoints:
    /:
        url: [author-instance-url]/bin/franklin.delivery/[Github owner]/[Github Repository]/[Github branch] 
        type: "markup"
        suffix: ".html"
   ```

   例如，如果您的 GitHub 存放庫名為 &quot;aemcrosswalk&quot; (位於帳戶 &quot;wkndform&quot; 下面)，並且您使用的是 &quot;main&quot; 分支，則作者執行個體 URL 會如下所示：

   ```
        mountpoints:
            /:
            url: https://author-p133911-e1313554.adobeaemcloud.com/bin/franklin.delivery/wkndform/aemcrosswalk/main
            type: "markup"
            suffix: ".html"
   ```

1. 認可對 `fstab.yaml` 檔案的變更。

### 將 AEM 執行個體連結到 GitHub 存放庫

若要將 AEM Forms 作者執行個體連結到[您在 GitHub 存放庫上的專案](/help/edge/docs/forms/tutorial.md)，請執行下列步驟：

[1. 根據 Edge Delivery Services 範本建立最適化表單](#1-create-an-adaptive-form-based-on-the-edge-delivery-services-template)

[2. 在 AEM 作者執行個體中找到表單的設定容器](#2-locate-your-forms-configuration-container-in-aem-author-instance)

[3. 在通用編輯器中編寫表單](#3-author-the-form-in-the-universal-editor)

[4. 發佈和預覽表單](#4-publish-and-preview-the-form)

#### 1. 根據 Edge Delivery Services 範本建立最適化表單

1. 存取您的 AEM Forms 作為雲端服務作者執行個體。
1.  選取 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**。1. 選取&#x200B;**[!UICONTROL 建立]**  > **[!UICONTROL 最適化表單]**。此時會開啟精靈。在「來源」索引標籤中，選擇根據 Edge Delivery Services 的 formtemplate：

   ![建立 EDS Forms](/help/edge/assets/create-eds-forms.png){width=50%, align-center}

1. 按一下&#x200B;**[!UICONTROL 建立]**，即會出現&#x200B;**建立表單**&#x200B;精靈。
1. 指定 **GitHub URL**。例如，如果您的 GitHub 存放庫名為 “aemcrosswalk” (位於帳戶 “wkndform” 下面)，則 URL 為：
   `https://github.com/wkndform/aemcrosswalk`
1. 按一下&#x200B;**[!UICONTROL 建立]**。

   ![建立表單精靈](/help/edge/assets/create-form-wizard.png){width=50%, align-center}

   您按一下&#x200B;**[!UICONTROL 建立]**，表單即會在通用編輯器中開啟以供編寫。

   ![編寫表單](/help/edge/assets/author-form.png){width=50%, align-center}

   >[!NOTE]
   >
   > 根據 Edge Delivery Services 範本的表單的 Edge Delivery Services 設定會在表單的設定容器中自動建立。

#### 2. 在 AEM 作者執行個體中找到表單的設定容器

1. 在您的 AEM Forms 作為雲端服務作者執行個體上，瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Edge Delivery Services 設定]**。
1. 選取與表單名稱相符的資料夾。例如，如果您的表單稱為 “contact-us”，請選擇資料夾 `forms/contact-us` 並選取設定和發佈設定：

   ![Edge Delivery Services 設定](/help/forms/assets/aem-instance-eds-configuration.png){width=50%, align-center}

1. 按一下&#x200B;**[!UICONTROL 屬性]**，以查看設定。\
   ![自動建立的設定](/help/edge/assets/aem-forms-create-configuration-github.png){width=50%, align-center}

   您可以將 Edge Host 選項保留不變。該表單會發佈到預覽 (.page) 和即時 (.live) 環境。

1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**。設定已儲存。

#### 3. 在通用編輯器中編寫表單

當您按一下&#x200B;**[!UICONTROL 建立]**&#x200B;時，表單即會在通用編輯器中開啟以供編寫。

1. 開啟內容瀏覽器，然後瀏覽至&#x200B;**[!UICONTROL 最適化表單]**&#x200B;元件 (在&#x200B;**內容樹**&#x200B;中)。

   ![內容樹](/help/edge/assets/content-tree.png){width=50%, align-center}

1. 按一下&#x200B;**[!UICONTROL 新增]**&#x200B;圖示，然後從&#x200B;**最適化表單元件**&#x200B;清單新增所需元件。

   ![新增元件](/help/edge/assets/add-component.png){width=50%, align-center}

1. 選取新增的最適化表單元件並使用&#x200B;**[!UICONTROL 屬性]**&#x200B;更新其屬性。

   ![開啟屬性](/help/edge/assets/component-properties.png){width=50%, align-center}

   下列螢幕擷取畫面會顯示在通用編輯器中編寫的簡單「聯絡我們」表單：

   ![聯絡我們表單](/help/edge/assets/contact-us.png){width=50%, align-center}

#### 4. 發佈和預覽表單

現在，按一下通用編輯器右上角的&#x200B;**[!UICONTROL 發佈]**&#x200B;按鈕，即可將表單發佈到 Edge Delivery Services。

![發佈表單](/help/edge/assets/publish-form.png){width=50%, align-center}


以下是存取 Edge Delivery Services 上的表單的方法：

* **暫存版本 (用於測試)**：暫存版本會顯示表單未發佈的工作版本，以用於測試目的。使用下列 URL 格式在表單上線之前預覽表單：

  `https://<branch>--<repo>--<owner>.aem.page/content/forms/af/<form_name>`

  例如，如果您的專案存放庫名為 &quot;aemcrosswalk&quot; (位於帳戶 &quot;wkndform&quot; 下面)，並且您使用的是 &quot;main&quot; 分支和 &quot;contact us&quot; 表單，則暫存版本 URL 會如下所示：https://main--aemcrosswalk--wkndform.aem.page/content/forms/af/contact-us

* **即時版本 (發佈形式)**：即時版本會顯示表單的最新發佈版本，可供終端使用者存取。使用以下 URL 格式存取表單的已發佈即時版本：

  `https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>`

  例如，如果您的專案存放庫名為 &quot;aemcrosswalk&quot; (位於帳戶 &quot;wkndform&quot; 下面)，並且您使用的是 &quot;main&quot; 分支和 &quot;contact us&quot; 表單，則暫存版本 URL 會如下所示：https://main--aemcrosswalk--wkndform.aem.live/content/forms/af/contact-us

暫存和即時版本的 URL 結構都保持不變。但是，您看到的內容會根據內容而有所不同：

![檢視已發佈表單](/help/edge/assets/eds-view-publish-form.png){width=50%, align-center}

## 疑難排解

載入表單時是否遇到問題？以下是一些常見問題以及修正的方法：

* **表單 URL**：仔細確認您表單的 URL 尾端並未包括副檔名 &quot;.html&quot;。Edge Deliver Service 不需要此副檔名。

* **AEM 作者 UR** L：確保 `fstab.yaml` 檔案中所列的 AEM 作者 URL 格式正確。它應包括下列詳細資料：

   * 正確的 GitHub 所有者
   * 正確的存放庫名稱
   * 您用於 Edge Delivery Services 的特定分支

<!-- * **JSON Display**: If you see only JSON data instead of the actual form, your form block might be outdated. You can update it to the latest version available on https://github.com/adobe-rnd/aem-boilerplate-forms.
-->

## 另請參閱

{{see-more-forms-eds}}
