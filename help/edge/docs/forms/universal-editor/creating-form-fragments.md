---
title: 如何建立 WYSIWYG 型編寫適用的表單片段
description: 了解如何在通用編輯器中建立表單片段，並將其新增至表單。
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: ht
source-wordcount: '1693'
ht-degree: 100%

---

# 在通用編輯器中建立表單片段

表單片段是可重複使用的元件，能免除重複性開發工作並確保組織內的表單維持一致性。與其針對每個表單重新建立如聯絡資訊、地址詳細資訊或同意協議之類的通用區段，您可以將這些元素建置為片段一次，然後在多個表單中重複使用。

**您在本文中會實現的目標：**

- 了解表單片段的商業價值與技術能力
- 使用通用編輯器建立可重複使用的表單片段
- 透過正確的設定將片段與現有表單整合
- 管理片段生命週期及維持表單間的一致性

**商業利益：**

- **縮短開發時間**：只要建置一次通用的表單區段，即可在任何地方重複使用
- **提升一致性**：將所有表單的版面和內容標準化
- **簡化維護過程**：只要更新片段一次，即可在使用該片段的所有表單反映變更
- **增強合規性**：確保監管區段保持一致且為最新版本

Edge Delivery Services 中的表單片段支援多項進階功能，包括巢狀片段、單一表單中有多個實例，以及與資料來源的緊密整合。

## 了解表單片段

Edge Delivery Services 中的表單片段為模組化表單開發提供強大的功能：

**核心功能：**

- **一致性管理**：片段可讓多個表單維持相同的版面和內容。透過「一次變更，全面反映」的方法，在預覽模式中，對片段進行更新會自動套用至所有表單。
- **多種用途**：在單一表單中多次新增相同的片段，每個片段都會建立獨立的資料繫結，連結到不同的資料來源或結構描述元素。
- **巢狀結構**：將片段嵌入其他片段中，建立複雜的階層，形成複雜的表單架構。

**技術需求：**

- **GitHub URL 一致性**：片段及使用片表的任何表單都必須指定相同的 GitHub 存放庫 URL
- **獨立編輯**：片段只能單獨修改；無法在主版表單中進行變更

**發佈行為：**

>[!IMPORTANT]
>
>在預覽模式下，片段變更會立即反映在所有表單上。在發佈模式下，您必須重新發佈片段及使用該片段的任何表單才能看到更新。

>[!CAUTION]
>
>避免遞迴式的片段參照 (將片段巢狀嵌入自身之中)，因為這會導致轉譯錯誤和非預期行為。

## 先決條件

**技術設定需求：**

- [GitHub 存放庫已設定](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)，而且在您的 AEM 環境與 GitHub 存放庫之間建立連線
- 將[最新的自適應表單區塊](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)新增至您的 GitHub 存放庫 (適用於現有的 Edge Delivery Services 專案)
- AEM Forms 作者實例，且有可用的 Edge Delivery Services 範本
- 您的 AEM Forms as a Cloud Service 作者實例 URL 和 GitHub 存放庫 URL 的存取權

**必要的知識與權限：**

- 對於表單設計概念和元件階層有基本認識
- 熟悉通用編輯器介面和表單建立工作流程
- 擁有 AEM Forms 的作者層級權限，以便建立和管理表單資產
- 對於您組織的表單標準和可重複使用元件的需求有所了解

## 使用 Edge Delivery Services 表單片段

您可以在通用編輯器中建立 Edge Delivery Services 表單片段，並將所建立的片段新增至 Edge Delivery Services 表單。您可以使用 Edge Delivery Services 表單片段執行下列動作：

- [在通用編輯器中建立表單片段](#creating-form-fragments-in-universal-editor)
   - [了解表單片段](#understanding-form-fragments)
   - [先決條件](#prerequisites)
   - [使用 Edge Delivery Services 表單片段](#working-with-edge-delivery-services-form-fragments)
   - [最佳做法](#best-practices)
   - [摘要](#summary)

+++ 建立表單片段

若要在通用編輯器中建立表單片段，請執行下列步驟：

1. 登入您的 AEM Forms as a Cloud Service 作者實例。
1. 選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。
1. 按一下「**建立 > 自適應表單片段**」。

   ![建立片段](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   將會出現「**建立自適應表單片段**」精靈。
1. 從「**選取範本**」索引標籤中選取以 Edge Delivery Services 為基礎的範本，然後按一下「**[!UICONTROL 下一步]**」。
   ![選取 Edge Delivery Services 範本](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. 指定片段的標題、名稱、描述和標記。確保為片段指定唯一的名稱。如果已存在名稱相同的片段，將無法建立片段。
1. 指定 **GitHub URL**。例如，若您的 GitHub 存放庫名稱為 `edsforms`，便是位在帳戶 `wkndforms` 之下，則 URL 為：`https://github.com/wkndforms/edsforms`。

   ![基本屬性](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (選擇性) 按一下以開啟「**表單模型**」標籤，接著從「**選取表單**」下拉式選單中選取下列其中一種片段模型：

   ![在「表單模型」標籤中顯示模型類型](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   - **表單資料模型 (FDM)**：將來自資料來源的資料模型物件和服務整合至您的片段中。若您的表單需要從多個來源讀取和寫入資料，請選擇表單資料模型 (FDM)。

   - **JSON 綱要**：透過與定義資料結構的 JSON 綱要建立關聯，將表單與後端系統整合。整合後您便能使用綱要元素新增動態內容。
   - **無模型**：指定此選項，即可不使用任何表單模型，從頭開始建立表單。

   >[!NOTE]
   >
   > 若要了解如何在通用編輯器中將表單或片段與表單資料模型 (FDM) 整合以使用不同的後端資料來源，請參閱[在通用編輯器中將表單與表單資料模型整合](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)。

1. (選用) 在「**進階**」標籤中，指定片段的「**發佈日期**」或「**取消發佈日期**」。

   ![「進階」標籤](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. 按一下「**建立**」來產生片段。接著出現具有編輯選項的成功對話框。

   ![編輯片段](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. 按一下「**編輯**」，在通用編輯器中開啟片段並套用預設範本。

   ![通用編輯器中要進行製作的片段](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

1. **設計片段內容**：新增表單元件 (文字欄位、下拉式選單、核取方塊)，建置可重複使用的區段。如需詳細的元件指引，請參閱[使用通用編輯器開始使用 AEM Forms 適用的 Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)。

1. **設定元件屬性**：根據您的使用案例之需求，設定欄位名稱、驗證規則和預設值。

1. **儲存及預覽**：儲存您的片段並使用預覽模式驗證版面和功能。

   ![通用編輯器中已完成之聯絡人詳細資料表單片段的螢幕擷圖，顯示可在多個表單中重複使用的姓名、電話、電子郵件及地址欄位](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

**驗證查核點：**

- 通用編輯器中片段載入無錯誤
- 所有表單元件均正確轉譯
- 欄位屬性和驗證規則如預期運作
- 片段已儲存並且可在「表單與文件」控制台中使用

片段完成後，您可以[將其整合至任何 Edge Delivery Services 表單中](#adding-form-fragments-to-a-form)。

+++


+++ 在表單中新增表單片段

此範例示範建立 `Employee Details` 表單並使用 `Contact Details` 片段作為員工和主管資訊區段。此方法可以確保資料彙集的一致性，同時減少開發工作量。

若要將表單片段整合至您的表單中：

1. 以編輯模式開啟表單。
1. 將表單片段元件新增至表單。
1. 開啟內容瀏覽器，然後導覽至「**內容樹**」中的&#x200B;**[!UICONTROL 自適應表單]**&#x200B;元件。
1. 導覽至您想要新增片段的區段。例如，導覽至「**員工詳細資訊**」面板。

   ![導覽至區段](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. 按一下「**[!UICONTROL 新增]**」圖示，然後新增來自「**自適應表單元件**」清單的&#x200B;**[!UICONTROL 表單片段]**元件。
   ![新增表單片段](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   選取&#x200B;**[!UICONTROL 表單片段]**&#x200B;元件後，片段即會新增至您的表單中。您可以開啟片段的「**屬性**」來設定新增片段的屬性。例如，在「**屬性**」中隱藏片段的標題。

   ![設定片段屬性](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. 在「**基本**」標籤中，選取「**片段參考**」。系統將會根據表單模型，顯示所有可供表單使用的片段。

   例如，導覽至 `/content/forms/af` 並選取 `Contact Details` 片段。

   ![選取片段](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. 按一下「**[!UICONTROL 選取]**」。

   以參照方式將表單片段新增至表單，並與獨立的表單片段保持同步。

   ![螢幕擷圖顯示聯絡人詳細資訊片段已成功整合至通用編輯器的員工表單中，並顯示片段在重複使用時如何保持其結構](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   >[!NOTE]
   >
   > 「**編輯片段**」按鈕可讓使用者直接導覽至表格片段以進行編輯。

   您可以透過&#x200B;**預覽**&#x200B;模式預覽表單的呈現效果。

   ![預覽](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   同樣地，您可以重複步驟 3 至 7，在 `Supervisor Details` 面板中插入 `Contact Details` 片段。

   ![員工詳細資料表單](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

+++



+++ 管理表單片段

您可以透過 AEM Forms 的使用者介面執行多項表單片段操作。

1. 登入您的 AEM Forms as a Cloud Service 作者實例。
1. 選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。

1. 選取表單片段，然後工具列便會顯示您可以對所選片段執行的操作。

   ![管理片段](/help/edge/docs/forms/universal-editor/assets/manage-fragment.png)

   <table>
    <tbody>
    <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
    </tr>
    <tr>
   <td><p>編輯</p> </td>
   <td><p>以編輯模式開啟表單片段。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>屬性</p> </td>
   <td><p>您可以選擇修改表單片段屬性。<br /> <br /> </p> </td>
    </tr>
    <td><p>複製</p> </td>
   <td><p> 您可以選擇複製表單片段，並將其貼上至所需位置。<br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>預覽</p> </td>
   <td><p>您可以選擇以 HTML 格式預覽片段，或是將 XML 檔案中的資料與片段合併來執行自訂預覽。<br /> </p> </td>
    </tr>
    <tr>
   <td><p>下載</p> </td>
   <td><p>下載所選片段。<br /><br /> </p> </td>
    </tr>
    <tr>
   <td><p>開始評論/管理評論</p> </td>
   <td><p>能啟動和管理所選片段的評論。<br /> <br /> </p> </td>
    </tr>
    <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
    </tr>-->
    <tr>
   <td><p>發佈/取消發佈</p> </td>
   <td><p>發佈/取消發佈所選片段。<br /><br /> </p> </td>
    </tr>
    <tr>
   <td><p>刪除</p> </td>
   <td><p>刪除所選片段。<br /><br /> </p> </td>
    </tr>
    <tr>
   <td><p>比較</p> </td>
   <td><p>比較兩種不同的表單片段以進行預覽。<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

+++ 

## 最佳做法

**片段設計與命名：**

- **使用描述性的唯一名稱**：選擇能夠清楚表明片段用途的名稱 (例如，「contact-details-with-validation」而非「fragment1」)
- **規劃重複使用性**：將片段設計為與內容無關，使其能夠適用於不同類型的表單
- **保持片段專一性**：建立單一用途的片段，而非複雜的多功能元件

**開發工作流程：**

- **片段獨立測試**：在片段與表單整合之前驗證其功能
- **維持一致的 GitHub URL**：確保所有相關片段和表單皆使用相同的存放庫 URL
- **文件片段用途**：包含清晰的說明和標記，協助團隊成員了解各片段應於何時使用

**發佈與維護：**

- **協調發佈**：更新片段時，規劃同時重新發佈所有相依的表單
- **版本控制**：更新片段時使用有意義的提交訊息，藉以追蹤一段時間內的變更
- **監視相依性**：追蹤哪些表單使用各個片段，以便評估更新的影響

>[!TIP]
>
>嵌入時，片段樣式、指令碼和運算式均會保留，因此設計時請留意這樣的繼承關係。

## 摘要

您已成功了解如何善用 Edge Delivery Services 中的表單片段來提升開發效率，並維持組織中各種表單的一致性。

**主要成就：**

- **了解**：掌握表單片段的商業價值與技術能力
- **建立**：使用通用編輯器搭配正確的設定，建置可重複使用的表單片段
- **整合**：利用正確的參照設定和屬性設定，在表單中新增片段
- **管理**：探索片段生命週期操作與維護工作流程

**後續步驟：**

- 建立您組織的常用片段資料庫。
- 建立使用片段所需的命名慣例與治理原則。
- 探索與[表單資料模型](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)的進階整合，以利使用資料驅動的動態片段
- 實作片段型表單範本，以實現一致的使用者體驗。

您的表單現在因為使用模組化且可維護的架構，能夠在多個專案之間有效擴展，同時確保一致的使用者體驗。


