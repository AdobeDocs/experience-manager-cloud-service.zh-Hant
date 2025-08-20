---
title: 如何建立 WYSIWYG 型編寫適用的表單片段
description: 了解如何在通用編輯器中建立表單片段，並將其新增至表單。
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 44%

---

# 在通用編輯器中建立表單片段

表單片段是可重複使用的元件，可消除重複開發工作並確保組織表單間的一致性。 您可以將這些元素建置為片段，並在多個表單中重複使用，而不是為每個表單重新建立常見區段，例如聯絡資訊、地址詳細資訊或同意協定。

**您將在本文中完成的內容：**

- 瞭解表單片段的商業價值和技術功能
- 使用通用編輯器建立可重複使用的表單片段
- 使用適當的設定將片段整合到現有表單中
- 管理片段生命週期並維護各表單的一致性

**企業福利：**

- **縮短開發時間**：一次建置通用表單區段，隨處重複使用
- **已改善一致性**：所有表單的標準化版面配置和內容
- **簡化維護作業**：更新片段一次，以反映使用片段的所有表單的變更
- **增強法規遵循性**：確保法規區段保持一致且為最新狀態

Edge Delivery Services中的表單片段支援進階功能，包括巢狀片段、單一表單內的多個執行個體以及與資料來源無縫整合。

## 瞭解表單片段

Edge Delivery Services中的表單片段提供模組化表單開發的強大功能：

**核心功能：**

- **一致性管理**：片段在多個表單中維持相同的版面和內容。 透過「變更一次，隨處反映」方法，片段的更新會自動套用至預覽模式中的所有表單。
- **多種用法**：在單一表單中多次新增相同的片段，每個片段都有到不同資料來源或結構描述元素的獨立資料繫結。
- **巢狀結構**：將片段內嵌於複雜表單架構的其他片段中，以建立複雜的階層。

**技術需求：**

- **GitHub URL一致性**：片段與任何使用它的表單都必須指定相同的GitHub存放庫URL
- **獨立編輯**：片段只能以獨立形式修改；無法在主機表單中進行變更

**發佈行為：**

>[!IMPORTANT]
>
>在預覽模式中，片段變更會立即反映在所有表單中。 在發佈模式中，您必須重新發佈片段及任何使用它來檢視更新的表單。

>[!CAUTION]
>
>避免遞回片段參考（在其內部巢狀內嵌片段），因為這會造成轉譯錯誤和意外行為。

## 先決條件

**技術設定需求：**

- [已設定GitHub存放庫](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)，且您的AEM環境與GitHub存放庫之間已建立連線
- [最新最適化Forms區塊](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)已新增到您的GitHub存放庫(適用於現有Edge Delivery Services專案)
- 提供具有Edge Delivery Services範本的AEM Forms作者例項
- 存取您的AEM Forms as a Cloud Service作者執行個體URL和GitHub存放庫URL

**必要的知識與許可權：**

- 基本瞭解表單設計概念和元件階層
- 熟悉通用編輯器介面和表單建立工作流程
- 在AEM Forms中建立和管理表單資產的作者層級許可權
- 瞭解貴組織的表單標準及可重複使用的元件需求

## 使用 Edge Delivery Services 表單片段

您可以在通用編輯器中建立 Edge Delivery Services 表單片段，並將所建立的片段新增至 Edge Delivery Services 表單。您可以使用 Edge Delivery Services 表單片段執行下列動作：

- [建立表單片段](#creating-form-fragments)
- [在表單中新增表單片段](#adding-form-fragments-to-a-form)
- [管理表單片段](#managing-form-fragments)

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
1. 指定 **GitHub URL**。例如，如果您的GitHub存放庫名為`edsforms`，則位於帳戶`wkndforms`下，URL為`https://github.com/wkndforms/edsforms`。

   ![基本屬性](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (選擇性) 按一下以開啟「**表單模型**」標籤，接著從「**選取表單**」下拉式選單中選取下列其中一種片段模型：

   ![在「表單模型」標籤中顯示模型類型](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   - **表單資料模型 (FDM)**：將來自資料來源的資料模型物件和服務整合至您的片段中。若您的表單需要從多個來源讀取和寫入資料，請選擇表單資料模型 (FDM)。

   - **JSON 綱要**：透過與定義資料結構的 JSON 綱要建立關聯，將表單與後端系統整合。整合後您便能使用綱要元素新增動態內容。
   - **無模型**：指定此選項，即可不使用任何表單模型，從頭開始建立表單。

   >[!NOTE]
   >
   > 若要了解如何在通用編輯器中將表單或片段與表單資料模型 (FDM) 整合以使用不同的後端資料來源，請參閱[在通用編輯器中將表單與表單資料模型整合](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)。

1. (選擇性) 在「**進階**」標籤中指定片段的「**發佈日期**」或「**取消發佈日期**」。

   ![進階索引標籤](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. 按一下&#x200B;**建立**&#x200B;以產生片段。 成功對話方塊隨即出現，其中包含編輯選項。

   ![編輯片段](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. 按一下「**編輯**」以在「通用編輯器」中開啟已套用預設範本的片段。

   通用編輯器中的![片段以供編寫](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

1. **設計您的片段內容**：新增表單元件（文字欄位、下拉清單、核取方塊）以建立可重複使用的區段。 如需詳細的元件指引，請參閱[使用通用編輯器的AEM FormsEdge Delivery Services快速入門](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)。

1. **設定元件屬性**：視使用案例需要設定欄位名稱、驗證規則和預設值。

1. **儲存並預覽**：儲存您的片段，並使用預覽模式來驗證版面配置和功能。

   ![通用編輯器中已完成的聯絡人詳細資訊表單片段之螢幕擷圖，顯示可在多個表單中重複使用的姓名、電話、電子郵件及地址](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

**驗證檢查點：**

- 片段在通用編輯器中載入且未發生錯誤
- 所有表單元件皆可正確轉譯
- 欄位屬性和驗證規則如預期般運作
- 片段已儲存並可在Forms和檔案控制檯中使用

片段完成後，您可以[將其整合到任何Edge Delivery Services表單](#adding-form-fragments-to-a-form)。

+++


+++ 在表單中新增表單片段

此範例示範如何建立員工和主管資訊區段均使用`Employee Details`片段的`Contact Details`表單。 此方法可確保資料收集的一致性，同時降低開發工作量。

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

   表單片段會參照表單新增，並與獨立表單片段保持同步。

   ![螢幕擷圖顯示聯絡人詳細資訊片段已成功整合至通用編輯器的員工表單中，並展示片段在重複使用時如何保持其結構](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

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

**片段設計和命名：**

- **使用描述性、唯一的名稱**：選擇可清楚表示片段用途的名稱（例如「contact-details-with-validation」而非「fragment1」）
- **規劃可重複使用**：設計片段與內容無關，因此可跨不同的表單型別運作
- **讓片段保持焦點**：建立單一用途的片段，而非複雜的多功能元件

**開發工作流程：**

- **獨立測試片段**：在整合至表單之前驗證片段功能
- **維持一致的GitHub URL**：確保在所有相關片段和表單中使用相同的存放庫URL
- **檔案片段用途**：包含清晰的說明和標籤，以協助團隊成員瞭解何時要使用每個片段

**發佈與維護：**

- **協調發佈**：更新片段時，計畫同時重新發佈所有相依表單
- **版本控制**：更新片段時請使用有意義的認可訊息來追蹤一段時間的變更
- **監視相依性**：追蹤使用每個片段來評估更新影響的表單

>[!TIP]
>
>片段樣式、指令碼和運算式在內嵌時會保留，因此在設計時會考慮這種繼承。

## 摘要

您已成功瞭解如何在Edge Delivery Services中運用表單片段來改善開發效率並維持組織表單的一致性。

**主要成績：**

- **瞭解**：掌握表單片段的商業價值和技術功能
- **建立**：使用具有適當組態的通用編輯器建置可重複使用的表單片段
- **整合**：新增片段至具有正確參考設定和屬性設定的表單
- **管理**：探索片段生命週期作業和維護工作流程

**後續步驟：**

- 為您的組織建立常用片段資料庫
- 為片段使用建立命名慣例和治理原則
- 探索與動態資料驅動片段的[表單資料模型](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)的進階整合
- 實作片段式表單範本，以維持一致的使用者體驗

您的表單現在受益於模組化、可維護的架構，該架構可在各個專案中有效擴展，同時確保一致的使用者體驗。


