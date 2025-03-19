---
title: 如何建立WYSIWYG式編寫的表單片段
description: 瞭解如何在通用編輯器中建立表單片段，並將其新增至表單。
feature: Edge Delivery Services
role: Admin, User, Developer
hide: true
hidefromtoc: true
source-git-commit: 62c58ceb2d2d659bad591b3eba1bfd924f2a848b
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 8%

---


# 在通用編輯器中建立和使用Edge Delivery Services表單片段

Forms通常包含聯絡資訊、身分識別詳細資訊或同意協定等常見區段。 表單開發人員每次建立新表單時都會建立這些區段，這是重複且耗時的。
為了消除這種重複勞動，Universal Editor提供了一種方法，只需建立一次可重複使用的表單區段（例如面板或欄位組），並在各種表單中重複使用。 這些可重複使用、模組化和獨立的區段稱為表單片段。 例如，相同的緊急聯絡人片段可用於表單的不同區段，例如員工和主管聯絡詳細資訊。

在文章結束時，您將瞭解如何使用通用編輯器在表單中建立和使用片段。

## Edge Delivery Services表單片段的功能

* **與表單片段保持一致性**
您可以將片段整合到不同的表單中，協助您維持一致的版面配置和標準化的內容。 透過「變更一次，隨處反映」方法，對片段所做的任何更新都會自動套用至所有表單。

* **在表單**中多次新增表單片段
您可以在表單中多次新增表單片段，並將其資料繫結屬性設定到資料來源或結構描述。

* **在片段中使用片段**
您可以建立巢狀表單片段，這表示您可以將片段新增到另一個片段中，而且可以有巢狀片段結構。

  >[!NOTE]
  >
  > 您無法在其內部巢狀內嵌片段，因為這樣可能會導致遞回參照和意外行為，進而導致錯誤或呈現問題。

## 使用Edge Delivery Services表單片段時的注意事項

* 您需要在片段和您打算使用片段的表單中，新增相同的GitHub URL。
* 您無法從表單中編輯透過參考插入的表單片段。 若要編輯，請修改獨立表單片段。

## 建立Edge Delivery Services表單片段的先決條件

* [設定您的 GitHub 存放庫](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)，在您的 AEM 環境與 GitHub 存放庫之間建立連線。
* 如果您已使用 Edge Delivery Services，請將最新版本的[最適化表單區塊](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)新增至您的 GitHub 存放庫。
* AEM 表單作者執行個體包括根據 Edge Delivery Services 建立的範本。請確保您的環境中安裝了[最新版本的核心元件](https://github.com/adobe/aem-core-forms-components)。
* 將 AEM Forms 作為雲端服務作者執行個體的 URL 和 GitHub 存放庫保持便於使用。

## 使用Edge Delivery Services表單片段

您可以在通用編輯器中建立Edge Delivery Services表單片段，並將建立的片段新增至Edge Delivery Services表單。 您可以使用Edge Delivery Services表單片段執行下列動作：

* [建立表單片段](#creating-form-fragments)
* [將表單片段新增至表單](#adding-form-fragments-to-a-form)
* [管理表單片段](#managing-form-fragments)

### 建立表單片段

若要在通用編輯器中建立表單片段，請執行以下步驟：

1. 登入AEM Forms as a Cloud Service作者例項。
1. 選取&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。
1. 按一下&#x200B;**建立>最適化表單片段**。

   ![建立片段](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   **建立最適化表單片段**&#x200B;精靈出現。
1. 從&#x200B;**選取範本**&#x200B;索引標籤中選取Egde傳遞服務型範本，然後按一下&#x200B;**[!UICONTROL 下一步]**。
   ![選取Edge Delivery Services範本](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. 指定片段的標題、名稱、說明和標籤。 請確定您為片段指定唯一的名稱。 如果存在具有相同名稱的其他片段，則無法建立片段。
1. 指定 **GitHub URL**。例如，如果您的GitHub存放庫名為`edsforms`，則位於帳戶`wkndforms`下，URL為`https://github.com/wkndforms/edsforms`。

   ![基本屬性](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. （選擇性）按一下以開啟&#x200B;**表單模型**&#x200B;標籤，然後從&#x200B;**選取自**&#x200B;下拉式功能表中，為片段選取下列其中一個模型：

   ![在表單模型索引標籤中顯示模型型別](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   * **表單資料模型(FDM)**：將資料來源中的資料模型物件和服務整合到您的片段中。 如果您的表單需要從多個來源讀取和寫入資料，請選擇「表單資料模型(FDM)」。

   * **JSON結構描述**：關聯定義資料結構的JSON結構描述，將您的表單與後端系統整合。 它可讓您使用結構元素來新增動態內容。
   * **無**：指定從頭開始建立片段，而不使用任何表單模型。

   >[!NOTE]
   >
   > 若要瞭解如何將表單或片段與Universal Editor中的表單資料模型(FDM)整合，以使用不同的後端資料來源，請[按一下這裡](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)。

1. （選擇性）在&#x200B;**進階**&#x200B;索引標籤中指定片段的&#x200B;**發佈日期**&#x200B;或&#x200B;**取消發佈日期**。

   ![進階索引標籤](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. 按一下&#x200B;**建立**，精靈就會出現。

   ![編輯片段](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. 按一下「**編輯**」，使用預設範本建立的片段就會在Universal Editor中開啟以進行編寫。

   在Universal Editor中用於編寫的![片段](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

   在編輯模式中，您可以將任何表單元件新增到片段。 若要瞭解如何在通用編輯器中建立片段，請參閱[使用通用編輯器的AEM FormsEdge Delivery Services快速入門](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)文章。

   以下熒幕擷圖顯示在Universal Editor中建立的`contact fragment`。

   ![連絡人片段](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

   建立片段後，您可以[在Edge Delivery Services Forms中新增建立的片段](#adding-form-fragments-in-forms)。

### 將表單片段新增至表單

讓我們建立包含員工和主管資訊的簡單`Employee Details`表單。 您可以在員工和主管面板中使用`Contact Details`片段。 若要在您的表單中使用表單片段，請執行以下步驟：

1. 在編輯模式中開啟表單。
1. 將表單片段元件新增至表單。
1. 開啟內容瀏覽器，然後導覽至&#x200B;**內容樹**&#x200B;中的&#x200B;**[!UICONTROL 自適應表單]**&#x200B;元件。
1. 導覽至您要新增片段的區段。 例如，瀏覽至&#x200B;**員工詳細資料**&#x200B;面板。

   ![瀏覽至區段](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. 按一下「**[!UICONTROL 新增]**」圖示，然後從&#x200B;**最適化表單元件**&#x200B;清單新增&#x200B;**[!UICONTROL 表單元件]**元件。
   ![新增表單片段](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   當您選取&#x200B;**[!UICONTROL 表單片段]**&#x200B;元件時，片段會新增至您的表單。 您可以透過開啟其&#x200B;**屬性**&#x200B;來設定新增片段的屬性。 例如，從片段的&#x200B;**屬性**&#x200B;隱藏片段的標題。

   ![正在設定片段](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)的內容

1. 在&#x200B;**基本**&#x200B;索引標籤中選取&#x200B;**片段參考**。 您的表單可用的所有片段都會出現，視表單的模型而定。

   例如，導覽至`/content/forms/af`並選取`Contact Details`片段。

   ![選取片段](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. 按一下&#x200B;**[!UICONTROL 選取]**。

   表單片段會參照表單新增，並與獨立表單片段保持同步。 這表示對片段所做的任何修改都會反映在片段合併到表單中的所有執行個體中。

   ![表單](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)中的片段

   您可以預覽表單，以檢視表單在&#x200B;**預覽**&#x200B;模式中的顯示方式。

   ![預覽](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   同樣地，您可以重複步驟3到7來插入`Supervisor Details`面板的`Contact Details`片段。

   ![員工詳細資料表單](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

### 管理表單片段

您可以使用AEM Forms使用者介面對表單片段執行數個操作。

1. 登入AEM Forms as a Cloud Service作者例項。
1. 選取&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**。

1. 選取表單片段，工具列會顯示您可對所選片段執行的下列操作。

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
   <td><p>提供修改表單片段屬性的選項。<br /> <br /> </p> </td>
    </tr>
    <td><p>複製</p> </td>
   <td><p> 提供複製表單片段並將其貼到所需位置的選項。<br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>預覽</p> </td>
   <td><p>提供以HTML預覽片段的選項，或透過將XML檔案中的資料與片段合併來執行自訂預覽。<br /> </p> </td>
    </tr>
    <tr>
   <td><p>下載</p> </td>
   <td><p>下載選取的片段。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>開始檢閱/管理檢閱</p> </td>
   <td><p>允許起始和管理所選片段的檢閱。<br /> <br /> </p> </td>
    </tr>
    <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
    </tr>-->
    <tr>
   <td><p>發佈/取消發佈</p> </td>
   <td><p>發佈/取消發佈選取的片段。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>刪除</p> </td>
   <td><p>刪除選取的片段。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>比較</p> </td>
   <td><p>比較兩個不同的表單片段以供預覽。<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

## 最佳做法

* 確保片段名稱是唯一的。 如果存在具有相同名稱的現有片段，則片段無法建立。
* 以參考方式插入或嵌入表單時，獨立表單片段中的任何運算式、指令碼或樣式都會保留。
* 當您發佈表單時，由表單內的參考插入的表單片段會自動發佈。

## 另請參閱

{{universal-editor-see-also}}