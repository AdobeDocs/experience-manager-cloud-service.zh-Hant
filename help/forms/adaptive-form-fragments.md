---
title: 如何建立及使用最適化表單片段？
description: 表單片段是表格的模組化且可重複使用的元件。 瞭解如何建立表單片段，並在各個表單中重複使用，以有效率地組合表單。
uuid: bb4830b5-82a0-4026-9dae-542daed10e6f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
exl-id: e4d8bcb9-ce1f-425e-b35c-d0a79fa771f3
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 1%

---

# 在最適化表單中建立和使用最適化Forms片段  {#adaptive-form-fragments}


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service （基礎元件） | 本文章 |
| AEM as a Cloud Service （核心元件） | [按一下這裡](/help/forms/adaptive-form-fragments-core-components.md) |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/adaptive-form-fragments.html?lang=en) |

雖然每個表單都是為特定目的而設計的，但大多數表單中有一些常見的部分，例如提供個人詳細資訊按讚姓名和位址、家庭詳細資訊、收入詳細資訊等。 每次建立新表單時，表單開發人員都必須建立這些通用區段。 自適應Forms提供了一種方便的機制，只需區段 按讚面板或字段群組創建表單一次，並在自適應Forms中重複使用它們。 這些可重複使用的獨立區段稱為「最適化表單片段」。


## 建立片段 {#create-a-fragment}

您可以從頭開始建立最適化表單片段，或將現有最適化表單中的面板儲存為片段。

### 從頭開始建立片段 {#create-fragment-from-scratch}

1. 登入 [!DNL AEM Forms] 作者執行個體 https://[*hostname*]：[*連接埠*]/aem/forms.html。
1. 按兩下 **建立 >最適化表單片段**。
1. 指定片段的標題、名稱、描述和標籤。

   >[!NOTE]
   >
   >請確定您為片段指定唯一的名稱。 如果已經有另一個相同名稱的片段，則無法建立片段。

1. 按一下以開啟 **表單模型** 標籤，並從 **選取自** 下拉式選單，為片段選取以下其中一個模型：

   * **無**：指定從頭開始建立片段，而不使用任何表單模型。

     >[!NOTE]
     >
     > 在Adaptive Forms中，您可以在表單中多次使用單一表單片段（根據核心元件）。 它支援無型和結構描述型表單片段。

   * **表單範本**：指定使用上傳至的XDP範本建立片段 [!DNL AEM Forms]. 選取適當的XDP範本作為片段的表單模型。

   ![使用表單範本作為模型建立調適型表單](assets/form-template-model.png)

   也會顯示所選表單範本中標籤為片段的子表單。 您可以從下拉式清單中選取最適化表單片段的子表單。

   ![從指定的表單範本中選取子表單](assets/fragment-subform.png)

   此外，您可以透過在下拉式方塊中指定子表單的SOM運算式，使用未在表單範本中標籤為片段的子表單來建立最適化表單片段。

   * **XML結構描述**：指定使用上傳至的XML結構描述建立片段 [!DNL AEM Forms]. 您可以上傳或從可用的XML結構描述中選取作為片段的表單模型。

   ![根據XML結構描述作為模型建立最適化表單片段](assets/xml-schema-model.png)

   您也可以從下拉式方塊選取所選結構描述中存在的complexType，以建立最適化表單片段。

   ![從指定的XML結構描述模型選取複雜型別](assets/complex-type.png)

1. 按一下 **建立** 然後按一下 **開啟** 以使用預設範本在編輯模式中開啟片段。

在編輯模式中，您可以將任何最適化表單元件從AEM sidekick拖放至片段上。 <!-- For information about Adaptive Form components, see Introduction to authoring Adaptive Forms. -->

此外，如果您選取XML結構描述或XDP表單範本作為片段的表單模型，內容尋找器中會出現一個顯示表單模型階層的新索引標籤。 它可讓您將表單模型元素拖放至片段上。 新增的表單模型元素會轉換為表單元件，同時保留關聯XDP或XSD的原始屬性。

### 將面板另存為片段 {#save-panel-as-a-fragment}

1. 開啟包含您要另存為最適化表單片段的面板的最適化表單。
1. 在面板工具列中，按一下 **[!UICONTROL 另存為片段]**. 另存為片段對話方塊隨即開啟。

   >[!NOTE]
   >
   >如果您要儲存為片段的面板包含子面板，則產生的片段將包含這些面板。

1. 在「片段建立」對話方塊中，指定下列資訊：

   * **名稱**：片段的名稱。 預設值為面板的元素名稱。 這是必填欄位。

     >[!NOTE]
     >
     >請確定您為片段指定唯一的名稱。 如果已經有另一個相同名稱的片段，則無法建立片段。

   * **標題**：片段的標題。 預設值為面板的標題。

   * **說明**：片段的說明。

   * **標籤**：片段的標籤中繼資料。

   * **目標路徑**：儲存片段的存放庫路徑。 若您未指定路徑，則會在包含最適化表單的節點旁建立與片段名稱相同的節點。 片段會儲存在此節點中。

   * **表單模型**：根據最適化表單的表單模型，此欄位會顯示 **XML結構描述**， **表單範本**，或 **無**. 這是不可編輯的欄位。

   * **片段模型根**：僅顯示在XSD型最適化Forms中。 它會指定片段模型的根。 您可以選擇 **/** 或下拉式清單中的XSD複雜型別。 只有在您選取複雜型別作為片段模型根時，才能在另一個Adaptive Form中重複使用片段。
如果您選擇 **/** 作為片段模型根，根的完整XSD樹狀結構顯示在Adaptive Form Data Model標籤中。 對於複雜型別片段模型根，在「最適化表單資料模型」索引標籤中只會顯示所選複雜型別的子系。

   * **XSD參照**：僅顯示在XSD型最適化Forms中。 它顯示XML綱要的位置。

   * **XDP參照**：僅顯示在XDP型最適化Forms中。 它顯示XDP表單範本的位置。

   ![save-fragment](assets/save-fragment.png)

   另存為片段對話方塊

1. 按一下&#x200B;**「確定」**。

   面板會儲存在存放庫中的指定或預設位置。 在調適型表單中，面板會由片段的快照取代。 如下所示，「一般資訊」面板及其子面板「個人資訊和地址」會儲存為片段。

   若要編輯片段，請按一下 **[!UICONTROL 編輯資產]** 在面板工具列中。 片段會在編輯模式的新標籤或視窗中開啟。

   ![編輯片段](assets/edit-fragment.png)

## 使用片段 {#working-with-fragments}

### 設定片段外觀 {#configure-fragment-appearance}

您在 Adaptive Forms 中插入的任何片段都會顯示為佔位元影像。 佔位元顯示片段中最多十個子面板的標題。 您可以設定 [!DNL AEM Forms] 顯示完整片段而非預留位置影像。

執行以下步驟，在表單中顯示完整的片段：

1. 前往AEM Web主控台設定頁面，網址為https：[*主機*]：[*連線埠*]/system/console/configMgr。

1. 搜尋並按一下 **[!UICONTROL 最適化表單設定服務]** 以編輯模式開啟。
1. 停用 **[!UICONTROL 啟用預留位置來取代片段]** 核取方塊以顯示完整的片段，而非預留位置影像。

### 在自適應表單中插入片段 {#insert-a-fragment-in-an-adaptive-form}

您建立的最適化窗体片段會显示在 AEM 內容 Finder 的「最適化窗体片段」標籤中。 要在最適化表單插入最適化表單片段：

1. 在編輯模式中開啟您要插入最適化表單片段的最適化表單。
1. 按一下 **Assets** ![資產 — 瀏覽器](assets/assets-browser.png) 在側邊欄中。 在資產瀏覽器中，選取 **最適化表單片段** 從下拉式清單。

   您也可以選擇顯示所有最適化表單片段，或根據其表單模型（表單範本、XML結構描述或基本）進行篩選。

1. 將最適化表單片段拖放至最適化表單上。

   >[!NOTE]
   >
   >未啟用最適化表單片段來從最適化表單內進行製作。 此外，您無法在JSON型最適化表單中使用XSD型片段，反之亦然。

最適化表單片段會以參考方式插入最適化表單片段中，並與獨立的最適化表單片段同步。 這表示當您更新最適化表單片段時，變更會反映在使用片段的所有Adaptive Forms中。

### 在自適應表單中嵌入片段 {#embed-a-fragment-in-adaptive-form}

您可以按一下「 」，選擇將最適化表單片段嵌入最適化表格中 **內嵌資產： &lt;*片段名稱*>** 按鈕時，按鈕會在已新增片段的面板工具列上，如下列範例影像所示。

![在最適化表單中嵌入表單片段](assets/embed-fragment.png)

>[!NOTE]
>
>嵌入的片段不再與獨立片段連結。 您可以從最適化表單內編輯內嵌片段中的元件。

### 在片段中使用片段 {#using-fragments-within-fragments}

您可以建立巢狀的Adaptive Form片段，這表示您可以將片段拖放到另一個片段中，而且可以有巢狀片段結構。

### 變更片段 {#change-fragments}

您可以使用來用其他片段取代或變更最適化表單片段 **選取片段資產** Adaptive Form片段面板的「編輯元件」對話方塊中的屬性。

### 在最適化表單中多次使用表單片段 {#using-form-fragment-mutiple-times-in-af}

您可以在調適型表單中多次使用結構描述型表單片段，以唯一儲存每個表單片段欄位的資料。 例如，您可以使用地址表單片段來收集地址詳細資訊，以便永久性、通訊和在貸款申請表中呈現有效地址。

![在最適化表單中使用多個片段](/help/forms/assets/using-multiple-fragment-af.gif)

>[!NOTE]
>
> 如果您在適用性表單中多次使用無架構表單片段，則會發生片段欄位之間的資料同步問題。 您可以使用 [基於核心元件的表單片段](/help/forms/adaptive-form-fragments-core-components.md) 未繫結到任何表單資料模型(FDM)，在表單中多次沒有遇到資料同步問題。

## 自動對應資料繫結的片段 {#auto-mapping-of-fragments-for-data-binding}

當您使用XFA表單範本或XSD複雜型別建立最適化表單片段，並將片段拖放至最適化表單時，XFA片段或XSD複雜型別會自動由對應的最適化表單片段取代，其片段模型根會對應至XFA片段或XSD複雜型別。

您可以從「編輯元件」對話方塊變更片段資產及其連結。

>[!NOTE]
>
>您也可以從AEM內容尋找器中的最適化表單片段資料庫拖放已繫結的最適化表單片段，並從Adaptive Form片段面板的「編輯」元件對話方塊提供正確的繫結參考。

## 管理片段 {#manage-fragments}

您可以使用對最適化表單片段執行數個操作 [!DNL AEM Forms] UI。

1. 前往 `https://[hostname]:'port'/aem/forms.html`。

1. 按一下 **選取** 在 [!DNL AEM Forms] UI工具列並選取最適化表單片段。 工具列會顯示您對選取的Adaptive Form片段可以執行的下列操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>開啟</p> </td>
   <td><p>在編輯模式中開啟所選的Adaptive Form片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>檢視屬性</p> </td>
   <td><p>開啟屬性面板。 從「屬性」面板中，您可以檢視和編輯屬性、產生預覽，以及上傳所選片段的縮圖影像。 如需詳細資訊，請參閱 <a href="manage-form-metadata.md" target="_blank">管理中繼資料</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>複製</p> </td>
   <td><p>複製所選片段。 「貼上」按鈕會出現在工具列中。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>下載</p> </td>
   <td><p>下載選取的片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>預覽</p> </td>
   <td><p>提供以HTML預覽片段的選項，或透過將XML檔案的資料與片段合併來預覽自訂預覽。 <!-- For more information, see <a href="previewing-forms.md" target="_blank">Previewing a form</a>.<br /> <br /> --></p> </td>
  </tr>
  <tr>
   <td><p>開始檢閱/管理檢閱</p> </td>
   <td><p>允許啟動和管理所選片段的審查。 <!-- For more information, see <a href="create-reviews-forms.md" target="_blank">Creating and managing reviews</a>.<br /> <br /> </p> --> </td>
  </tr>
  <tr>
   <td><p>建立字典</p> </td>
   <td><p>產生字典以將選取的片段本地化。 <!-- For more information, see <a href="lazy-loading-adaptive-forms.md" target="_blank">Localizing Adaptive Forms</a>.<br /> <br /> --> </p> </td>
  </tr>
  <tr>
   <td><p>Publish /取消發佈</p> </td>
   <td><p>發佈/取消發佈所選的片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>刪除</p> </td>
   <td><p>刪除選取的片段。<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## 當地語系化包含片段的最適化表單 {#localizing-adaptive-form-containing-fragments}

要本地化包含自適應表單片段的最適化表單，您需要分別當地語系化片段和表單。 這個想法是將片段當地語系化一次，然後在多個自適應Forms中重複使用。

>[!NOTE]
>
>片段中的本地化索引鍵不會出現在最適化表單的XLIFF檔案中。

## 使用片段時要記住的關鍵點 {#key-points-to-remember-when-working-with-fragments}

* 確保片段名稱是唯一的。 如果存在具有相同名稱的現有片段，則片段無法建立。
* 在基於 XDP 的自適應表單中，如果將面板另存為包含另一個 XDP 片段的片段，則生成的片段將自動綁定到子 XDP 片段。 如果是基於 XSD 的最適化表單，則生成的片段將綁定到綱要根目錄。
* 當您建立最適化窗體片段時，會建立片段節點，類似於CRXDe Lite中最適化窗體的 guideContainer 節點。
* 不支援使用不同表單資料模型 （FDM） 的自適應表單片段。 例如，基於 XDP 的自適應表單不支援基於 XDP 的片段，反之亦然。
* 最適化表單片段可透過AEM內容尋找器中的最適化表單片段標籤使用。
* 透過參考插入或嵌入自適應表單時，獨立自適應表單片段中的任何運算式、指令碼或樣式都會保留。
* 您無法從最適化表單中編輯透過參考插入的最適化表單片段。 若要編輯，請編輯獨立的Adaptive Form片段或將片段嵌入到Adaptive Form中。
* 發佈最適化表單時，您需要發佈在最適化表單中透過參考插入的獨立最適化表單片段。
* 當您重新發佈更新的Adaptive Form片段時，變更會反映在使用片段的Adaptive Form的已發佈例項中。
* 包含Verify元件的調適型表單不支援匿名使用者。 此外，不建議在自適應表單片段中使用驗證元件。
* （**僅限** Mac）為了確保表單片段功能在所有場景中都能完美運行，請將以下內容添加到 /private/etc/hosts 檔中：
  `127.0.0.1 <Host machine>`**主機：**&#x200B;部署的 [!DNL AEM Forms] Apple Mac 電腦。

<!--
## Reference Fragments {#reference-fragments}

Reference Adaptive Form Fragments that you can use to create your form are available. For more information, see [Reference Fragments](reference-adaptive-form-fragments.md).
-->

>[!MORELIKETHIS]
>
>* [核心元件中的 Adaptive Form 片段](/help/forms/adaptive-form-fragments-core-components.md)
