---
title: 如何建立 WYSIWYG 型編寫適用的表單片段
description: 了解如何在通用編輯器中建立表單片段，並將其新增至表單。
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 97%

---

# 在通用編輯器中建立表單片段

<!--
<span class="preview"> This feature is available through the early access program. To request access, send an email with your GitHub organization name and repository name from your official address to <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> . For example, if the repository URL is https://github.com/adobe/abc, the organization name is adobe and the repository name is abc.</span> 

<span class="preview"> This is a pre-release feature and accessible through our [pre-release channel](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>
-->

表單通常包括常見的區段，例如聯絡資訊、身分詳細資料或同意協議等。表單開發人員每次建置新表單時都要建立這些區段，這是不斷重複又耗時的過程。為了避免一再重複這些工作，通用編輯器會協助您建立可重複使用的表單部分 (如面板或欄位群組)，只需建立一次即可在各種表單中重複使用。這些可重複使用、模組化且獨立的區段即稱為表單片段。例如，您可以在表單的不同區段 (例如員工和主管的聯絡詳細資訊) 使用相同的緊急聯絡人片段。

在本文的最後，您將能了解如何使用通用編輯器在表單中建立和使用片段。

## Edge Delivery Services 表單片段的功能

- **利用表單片段維持一致性**
您可以將片段與不同的表單整合，幫助您維持一致的版面與標準化內容。

  >[!NOTE]
  >
  > 透過「一次變更，全面反映」的方法，對片段所做的任何更新都會在預覽模式下自動套用至所有表單。但是，在「發佈」模式下，您必須發佈該片段或重新發佈該表單才能反映變更。

- **在表單內多次新增表單片段**
您可以在表單內多次新增表單片段，並將其資料繫結屬性設定為資料來源或綱要。

- **在片段中使用片段**
您可以建立巢狀表單片段，表示您可以在一個片段中新增另一個片段，並且可以採用巢狀片段結構。

  >[!NOTE]
  >
  > 片段本身不能自行嵌套，這可能會導致遞迴參考和意外行為，從而導致錯誤或轉譯問題。

## 使用 Edge Delivery Services 表單片段時的考量事項

- 您必須在片段以及您預計使用該片段的表單中新增相同的 GitHub URL。
- 您不能編輯表單內的表單片段。若要進行變更，請修改獨立的表單片段。

## 先決條件

- [設定您的 GitHub 存放庫](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)，在您的 AEM 環境與 GitHub 存放庫之間建立連線。
- 如果您已使用 Edge Delivery Services，請將最新版本的[自適應表單區塊](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)新增至您的 GitHub 存放庫。
- AEM Forms 作者實例包括以 Edge Delivery Services 為基礎的範本。
- 把 AEM Forms as a Cloud Service 作者實例的 URL 和 GitHub 存放庫放在方便取用的位置。

## 使用 Edge Delivery Services 表單片段

您可以在通用編輯器中建立 Edge Delivery Services 表單片段，並將所建立的片段新增至 Edge Delivery Services 表單。您可以使用 Edge Delivery Services 表單片段執行下列動作：

- [建立表單片段](#creating-form-fragments)
- [在表單中新增表單片段](#adding-form-fragments-to-a-form)
- [管理表單片段](#managing-form-fragments)

### 建立表單片段

若要在通用編輯器中建立表單片段，請執行下列步驟：

1. 登入您的 AEM Forms as a Cloud Service 作者實例。
1. 選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。
1. 按一下「**建立 > 自適應表單片段**」。

   ![建立片段](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   將會出現「**建立自適應表單片段**」精靈。
1. 從「**選取範本**」索引標籤中選取以 Edge Delivery Services 為基礎的範本，然後按一下「**[!UICONTROL 下一步]**」。
   ![選取 Edge Delivery Services 範本](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. 指定片段的標題、名稱、描述和標記。確保為片段指定唯一的名稱。如果已存在名稱相同的片段，將無法建立片段。
1. 指定 **GitHub URL**。例如，若您的 GitHub 存放庫名稱為 `edsforms`、位於帳戶 `wkndforms` 之下，則 URL 為：`https://github.com/wkndforms/edsforms`。

   ![基本屬性](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. (選擇性) 按一下以開啟「**表單模型**」標籤，接著從「**選取表單**」下拉式選單中選取下列其中一種片段模型：

   ![在「表單模型」標籤中顯示模型類型](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   - **表單資料模型 (FDM)**：將來自資料來源的資料模型物件和服務整合至您的片段中。若您的表單需要從多個來源讀取和寫入資料，請選擇表單資料模型 (FDM)。

   - **JSON 綱要**：透過與定義資料結構的 JSON 綱要建立關聯，將表單與後端系統整合。整合後您便能使用綱要元素新增動態內容。
   - **無模型**：指定此選項，即可不使用任何表單模型，從頭開始建立表單。

   >[!NOTE]
   >
   > 若要瞭解如何將表單或片段與Universal Editor中的表單資料模型(FDM)整合，以使用不同的後端資料來源，請參閱[將表單與Universal Editor中的表單資料模型整合](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)。

1. (選擇性) 在「**進階**」標籤中指定片段的「**發佈日期**」或「**取消發佈日期**」。

   ![「進階」標籤](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. 按一下「**建立**」便會出現精靈。

   ![編輯片段](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. 按一下「**編輯**」，便會在通用編輯器中開啟使用預設範本建立的片段，以供進行編寫。

   ![通用編輯器中可供編寫的片段](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

   在編輯模式下，您可以將任何表單元件新增至片段中。若要了解如何在通用編輯器中建立片段，請參閱「[透過通用編輯器開始使用 AEM Forms 適用的 Edge Delivery Services](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)」一文。

   下方螢幕擷圖顯示在通用編輯器中建立的 `contact fragment`。

   ![通用編輯器中已完成的聯絡人詳細資訊表單片段之螢幕擷圖，顯示可在多個表單中重複使用的姓名、電話、電子郵件及地址](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

   建立片段後，您可以[在 Edge Delivery Services 表單中新增所建立的片段](#adding-form-fragments-in-forms)。

### 在表單中新增表單片段

建立一個包含員工和主管資訊的簡易 `Employee Details` 表單。您可以在員工和主管面板中使用相同的 `Contact Details` 片段。若要在表單中使用表單片段，請執行下列步驟：

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

   以參考方式將表單片段新增至表單，並與獨立的表單片段保持同步。

   ![螢幕擷圖顯示聯絡人詳細資訊片段已成功整合至通用編輯器的員工表單中，並展示片段在重複使用時如何保持其結構](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   您可以透過&#x200B;**預覽**&#x200B;模式預覽表單的呈現效果。

   ![預覽](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   同樣地，您可以重複步驟 3 至 7，在 `Supervisor Details` 面板中插入 `Contact Details` 片段。

   ![員工詳細資料表單](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

### 管理表單片段

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

## 最佳做法

- 確認片段使用唯一的名稱。如果現有片段擁有相同的名稱，則無法建立片段。
- 獨立表單片段中的任何運算式、指令碼或樣式，在以參考方式插入或嵌入表單時都會保留。
- 當您發佈表單時，表單內以參考方式插入的表單片段將自動發佈。


