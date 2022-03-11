---
title: 如何建立自適應表單模板？
description: 建立自適應表單模板以使用模板編輯器定義基本結構和初始內容。
exl-id: a882cba2-c621-4ff7-a972-c504641b5639
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1750'
ht-degree: 1%

---

# 建立自適應表單模板 {#adaptive-form-templates}

建立表單時，將添加欄位和元件以在編輯器中定義表單結構、內容和操作。 在 `guideRootPanel` 形式容器的。 使用模板編輯器，可以建立包含基本結構和初始內容的模板，作者可以使用這些結構和初始內容建立表單。

例如，您希望所有表單作者在註冊表單中都具有某些文本框、導航按鈕和提交按鈕。 您可以建立模板，其中包含作者可用於建立與其它登記表單一致的表單的元件。 當作者使用模板建立自適應表單時，新表單將繼承您在模板中指定的結構和元件。 模板編輯器允許您：

* 在結構層中添加表單的頁眉和頁腳元件。
* 提供窗體的初始內容。
* 指定主題「提交操作」。

您可以下載並安裝 [!DNL AEM Forms] 引用內容包 [軟體分發](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 門戶，用於將參考主題和模板導入到您的環境。

## 使用模板 {#working-with-templates}

通過導航至 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 常規]** > **[!UICONTROL 模板]**。 在此，這些模板按為可編輯模板啟用的資料夾進行組織。

Experience Manager提供一個全局資料夾來組織模板。 但是，預設情況下未啟用它。 您可以請求管理員啟用全局資料夾或為模板建立資料夾。 有關如何建立資料夾的詳細資訊，請參見 [模板資料夾](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/templates.html#editing-templates-template-authors)。

### 建立範本 {#create-template}

建立資料夾後，開啟該資料夾並執行以下步驟以建立模板：

1. 點擊 **[!UICONTROL 建立]** 資料夾中。
1. 在「選取模板類型」(Pick a Template Type)部分，選擇 **[!UICONTROL 自適應表單模板]** 點擊 **[!UICONTROL 下一個]**。

1. 在「模板詳細資訊」部分，提供模板標題並點擊 **[!UICONTROL 建立]**。
您還可以提供說明。

1. 點擊 **[!UICONTROL 完成]** 返回控制台，或點擊 **[!UICONTROL 開啟]** 開啟編輯器中的模板。

### 模板編輯器UI {#template-editor-ui}

開啟模板進行編輯時，可以看到以下編輯AEM器元件：

* **頁面工具欄**
包含以下選項：

   * **切換側面板**:用於顯示或隱藏邊欄。
   * **頁面資訊**:用於指定資訊，如發佈/取消發佈時間、縮略圖、客戶端庫、頁面策略和頁面設計客戶端庫。

   <!-- * **Emulator**: Lets you simulate and customize the look for different devices.-->
   * **模式選擇器：** 允許您更改模式。
您可以選擇 **[!UICONTROL 結構]** 模式， **[!UICONTROL 初始內容]**。 **[!UICONTROL 佈局控制項]** 的子菜單。 「結構」模式允許您添加和自定義頁眉和頁腳。 「初始內容」模式允許您自定義表單內容。
   * **預覽：** 用於預覽模板在發佈時的外觀。 可以使用「圖層選擇器」和「預覽」切換編輯和預覽模式。
* **提要欄：** 提供內容、屬性、資產和元件瀏覽器。
* **元件工具欄：** 選擇元件時，將看到一個工具欄，它允許您自定義元件。
* **頁面**:添加內容以建立模板的區域。

<!-- See [Introduction to authoring Adaptive Forms](introduction-forms-authoring.md) to understand the Touch UI editor. -->

### 編輯模板 {#editing-a-template}

使用兩個層建立「自適應表單」模板：

* 結構
* 初始內容

圖層選擇器位於螢幕右上角的「預覽」選項旁。

### 結構 {#structure}

在「模板編輯器」中選擇結構層時，可以在「自適應表單容器」的上下看到佈局容器。 作者可以將這些佈局容器用於頁眉和頁腳。 您可以添加、編輯或自定義頁眉和頁腳。 在「自適應表單容器」上方的佈局容器中拖放「自適應表單標題」元件，以自定義模板標題。 在「自適應表單容器」下的佈局容器中拖放「自適應表單頁腳」元件，以自定義模板頁腳。

![結構層中的佈局容器](assets/header-layer-selector.png)

在結構層中佈局容器

**答：** 標題元件的佈局容器 **B** 頁腳元件的佈局容器

在「自適應表單容器」上方的佈局容器中拖放「自適應表單標題」元件。 添加元件後，可以指定其屬性，以便添加徽標並提供其標題。

同樣，在「自適應表單容器」下的佈局容器中拖放頁腳元件時，可以提供版權資訊和公司詳細資訊。

![在「結構」層中添加頁眉和頁腳](assets/header-and-footer.png)

在「結構」層中添加頁眉和頁腳

#### 在結構層中鎖定/解鎖部件 {#locking-unlocking-components-in-the-structure-layer}

在編輯選定結構層的模板時，可以解鎖模板的頁眉和頁腳。 如果在模板中解鎖了元件，則表單作者可以在使用該模板的「自適應表單」中編輯該元件。 鎖定元件會阻止表單作者在「自適應表單」中編輯它。 「鎖定」選項在元件工具欄中可用。

例如，在模板中添加標題元件。 選擇元件時，可以在元件工具欄中看到鎖定選項。 通常，標題包括公司名稱和徽標，您不希望表單作者更改模板中的徽標和標題。 在使用模板建立並鎖定標題元件的自適應表單中，表單作者無法更改徽標和公司名稱。

>[!NOTE]
>
>不建議單獨鎖定或解鎖頭元件中的影像或徽標。 可以解除標頭元件的鎖定。

### 初始內容 {#initial-content}

選擇「初始內容」選項後，模板的「自適應表單容器」(Adaptive Form Container)將像「自適應表單」(Adaptive Form)一樣開啟以進行編輯。 與創作自適應表單一樣，您可以指定初始設定，如選擇主題和提交操作。

表單作者將其用作建立表單的基。 內容流結構在模板的「初始內容」層中指定。 要切換到編輯表單模板的初始內容，請在頁面工具欄的「預覽」之前，點擊 ![畫布下拉清單](assets/canvas-drop-down.png) **>** **[!UICONTROL 初始內容]**。


在「初始內容」層中，建立作者用作基礎的「自適應表單」模板。 建立模板與建立表單類似，您使用「提要欄」中可用的選項。 Sidebar提供內容、屬性、資產和元件瀏覽器。

<!-- See [Sidebar](introduction-forms-authoring.md#sidebar). -->

>[!NOTE]
>
>選擇「儲存內容」或「儲存PDF」作為「提交操作」時，您將獲得一個選項來指定儲存路徑。 如果在模板中指定路徑，則根據該路徑建立的所有表單都具有相同的路徑。 您可以指定正確的儲存路徑，或確保表單作者更新該路徑以防止每個表單中的資料儲存在同一位置。

#### 建立帶制表符和面板的自適應表單模板 {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

例如，要建立具有以下頁籤的模板：

* 一般資訊
* 專業資訊

您已在結構層中添加了徽標、提供了標題和頁腳。 鎖定頁眉和頁腳，以阻止表單作者在使用模板建立表單時編輯它們。

將圖層從「結構」更改為「初始內容」，然後開始向表單添加內容。 要建立頁籤式結構，請在「自適應表單」容器的guideRootPanel中添加子面板。 要添加面板：

* 可通過按一下 **[!UICONTROL +]** 按鈕 **[!UICONTROL 將元件拖動到此處]** 的雙曲餘切值。

* 您可以從邊欄的元件瀏覽器拖放面板元件。
* 可以添加 `guideRootPanel` 的子菜單。

要建立「一般資訊」和「專業資訊」頁籤，請在子面板中添加兩個面板 `guideRootPanel`。 選擇面板並點擊 ![招商](assets/configure-icon.svg) 開啟提要欄中的屬性。 將元素名稱更改為 `general-info` 和 `professional-info`及「一般資料」及「專業資料」。 在提要欄中，點擊內容以開啟內容瀏覽器。 在「表單對象」頁籤中，選擇 `guideRootPanel`。 在編輯器中，將選擇guideRootPanel。 點擊 ![招商](assets/configure-icon.svg) 的子菜單。 在「面板佈局」欄位中，選擇 **[!UICONTROL 頂部的頁籤]** 點擊 **[!UICONTROL 完成]**。 將應用頁籤式模板結構。

#### 在頁籤中添加內容 {#adding-content-in-tabs}

添加面板並將其結構為頁籤後，可在頁籤內添加欄位。 在編輯器中選擇頁籤時，可以 **[!UICONTROL 將元件拖動到此處]** 的雙曲餘切值。 可以拖放元件，如文本框、清單項和按鈕。 您可以從邊欄的元件瀏覽器拖放元件。

每個元件都具有增強資料捕獲和操作的屬性。 例如，您可以 **[!UICONTROL 必填欄位]** 元件的屬性。 您的作者可以指定客戶跳過填寫必填欄位時看到的消息。 在中指定消息 **[!UICONTROL 必填欄位消息]** 屬性。

在示例模板中，「一般資訊」頁籤中添加了「名稱」、「電話號碼」和「出生日期」欄位。 在「專業資訊」標籤中，添加「當前聘用」、「雇傭類型」、「教育資格」欄位。

添加欄位後，可以添加按鈕，如提交和重置。

### 啟用模板 {#enabling-the-template}

建立模板時，它將添加為草稿。 啟用模板以用於建立自適應Forms。 要啟用模板：

1. 導航到 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 工具]** > **[!UICONTROL 模板]**，然後開啟在其中建立模板的資料夾。

1. 您建立的模板標籤為「草稿」。
1. 選擇模板並點擊 **[!UICONTROL 啟用]** 的子菜單。
在建立自適應表單時，您可以在被要求選擇模板時看到列出的模板。

## 導入或導出模板 {#importing-or-exporting-a-template}

表單與其模板一起使用。 下載使用自定義模板建立的自適應表單時，不會下載該模板。 當您在其他 [!DNL AEM Forms] 實例，導入時沒有模板。 如果導入了表單，但其模板不可用，則不呈現該表單。 可以將自定義模板打包為 `/conf` 節點 `https://<server>:<port>/crx/packmgr`，並將其插入 [!DNL AEM Forms] 要上載表單的實例。 您也可以 [使用原型創AEM建模板並將其部署到Cloud Services實例](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/pages-templates.html#prerequisites)。

## 使用模板建立自適應表單 {#creating-an-adaptive-form-using-the-template}

建立並啟用模板後，在建立「自適應表單」時，該模板在表單管理器中可用。 要使用模板並建立自適應表單，請參見 [建立自適應窗體](creating-adaptive-form.md)。

<!--
## Change display option of out of the box templates  {#change-display-option-of-out-of-the-box-templates}

You can create custom templates for Adaptive Forms to define basic structure and initial content. [!DNL AEM Forms] also provides a set of out of the box template for Adaptive Forms. You can choose to show or hide the templates.

Perform the following steps to show and hide templates:

1. Log in to [!DNL AEM Forms] author instance and navigate to **[!UICONTROL Tools]** &gt; **[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   >[!NOTE]
   >
   >The URL of AEM web console is https://'[server]:[port]'/system/console/configMgr

1. Locate and open the **FormsManager Configuration** settings:

    * To show or hide out of the box Adaptive Forms template, check or uncheck the **Include Out of the box AF and AD Templates** option.
    * To show or hide out of the box Adaptive Form templates that were added in AEM 6.0 Forms or AEM 6.1 Forms releases but are now deprecated, check or uncheck the **Include AEM 6.0 AF Templates** option. If this option is checked, in order to take effect, it requires the **Include Out of the box AF and AD Templates** configuration to be enabled.

1. Click **Save**. The display options for the out of the box templates are changed. -->

## 建議 {#recommendations}

* 在模板編輯器中修改表單的屬性時，不要使用BindReference屬性。
* 如果要添加斷點，請在建立Adaptive Form模板時建立它。
有關斷點的詳細資訊，請參見 [響應佈局](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/features/responsive-layout.html#authoring)。
