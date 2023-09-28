---
title: 最適化表單片段
description: 最適化Forms提供一種機制，可建立在任何最適化表單中使用的表單區段（例如面板或欄位群組）。 您也可以將現有面板儲存為片段。
topic-tags: author
keywords: 新增最適化表單片段、最適化表單片段、建立表單片段、新增片段至最適化表單、管理片段
feature: Adaptive Forms
source-git-commit: 7c197be7819d6fcbf028237401d05236f90734d1
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 4%

---


# 最適化表單片段 {#adaptive-form-fragments}


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | 本文章 |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/adaptive-form-fragments.html) |

雖然每個表單都是為特定目的而設計，但大多數表單中都有一些常見的區段，例如提供個人詳細資訊，例如姓名和地址、家庭詳細資訊、收入詳細資訊。 每次建立新表單時，表單開發人員都必須建立這些通用區段。

最適化Forms提供一種便利的機制，讓您只需建立一次表單區段（例如面板或欄位群組），即可在最適化Forms中重複使用。 這些可重複使用的獨立區段稱為「最適化表單片段」。

表單片段可無縫整合至多種表單，精簡建立一致且專業外觀的表單。 表單片段透過「一次變更，處處反映」功能確保可重複性、標準化和品牌一致性。由於在一處進行的更新會自動傳播到使用這些片段的所有表單，因此可體驗更高的可維護性和效率。

您可以將片段多次新增到檔案，並使用其元件的資料繫結屬性將其連結到不同的資料來源或結構描述。 例如，您可以將相同的地址片段用於永久、通訊和帳單地址，並將其連線到資料來源或結構的不同欄位。

## 建立表單片段 {#create-a-fragment}

您可以從頭開始建立最適化表單片段，或將現有最適化表單中的面板儲存為片段。 若要建立表單片段：

1. 在https://登入您的AEM Forms執行個體&#x200B;[*主機名稱*]：[*連線埠*]/aem/forms.html.
1. 按一下 **建立 >最適化表單片段** 」。
1. 指定片段的標題、名稱、描述和標籤。 確保為片段指定唯一的名稱。 如果已存在另一個同名片段，則無法創建該片段。
1. 選取表單範本。 您可以為以核心元件為基礎的Adaptive Forms或基礎元件為基礎的Adaptive Forms建立表單片段。
   * 若要建立核心元件型表單的表單片段，請選取核心元件型範本。
   * 要為基於基礎元件的表單創建表單片段，請選擇基礎元件範本。 例如，/libs/fd/af/templateForFragment/defaultFragmentTemplate。

   為基於核心元件的表單創建表單片段時，請使用「選擇表單主題」選項選擇基於核心元件的主題。

1. 按一下以打開「 **表單模型** 」標籤，然後從「 **從中選擇** 」下拉清單中，為片段選擇以下模型之一：

   ![在表單模型標籤中顯示模型類型](assets/create-af-1-1.png)

   * **無** ：指定在不使用任何表單模型的情況下從頭開始創建片段。

     >[!NOTE]
     >
     >核心元件型片段比基礎元件型片段的優點在於，可以在單一適用性表單中使用未與任何表單模型繫結的多核心元件型片段。

   * **結構描述**：指定使用上傳至AEM Forms的XML或JSON結構描述建立片段。 您可以上傳或從可用的XML或JSON結構描述中選取作為片段的表單模型。 選取XML結構描述時，您也可以從以下專案選取所選結構描述中存在的complexType，以建立最適化表單片段： **[!UICONTROL XML結構描述複雜型別]** 下拉式方塊。 選取JSON結構描述時，您也可以從以下專案選取所選結構描述中存在的結構描述定義，以建立調適型表單片段： **[!UICONTROL json結構描述定義]** 下拉式方塊。
   * **表單資料模型**：指定使用表單資料模型建立片段。 您可以根據表單資料模型中只有一個資料模型物件來建立最適化表單片段。 展開表單資料模型定義下拉式清單。 它會列出指定表單資料模型中的所有資料模型物件。 從清單中選取資料模型物件。

   ![表單資料模式](assets/create-af-3.png)



1. 按一下 **建立** 然後按一下 **開啟** 以使用預設範本在編輯模式中開啟片段。 在編輯模式中，您可以將任何最適化表單元件新增到片段。

<!-- For information about Adaptive Form components, see [Introduction to authoring Adaptive Forms](../../forms/using/introduction-forms-authoring.md). --> 此外，如果您選取XML結構描述或XDP表單範本作為片段的表單模型，內容尋找器中會出現一個顯示表單模型階層的新索引標籤。 它可讓您將表單模型元素拖放至片段上。 新增的表單模型元素會轉換為表單元件，同時保留關聯XDP或XSD的原始屬性。

根據結構或表單資料模型建立自適應表單片段後，表單資料模型或結構元素會出現在Adaptive Form編輯器中，內容瀏覽器的「資料來源」標籤中。 您可以將表單模型元素拖放至片段上。 新增的表單模型元素會轉換為表單元件，同時保留關聯結構描述的原始屬性。


## 將片段新增至最適化表單 {#insert-a-fragment-in-an-adaptive-form}

若要將最適化表單片段新增至最適化表單：

1. 在編輯模式中開啟最適化表單。
1. 新增 **最適化表單片段** 元件至表單。
1. 按一下 **資產** 內容瀏覽器側欄。 在資產瀏覽器的路徑下，選取 **最適化表單片段** 選項。 您的表單可用的所有Adaptive Forms片段（視表單的模型而定）都會出現。

   ![選取最適化表單片段選項](assets/adaptive-forms-fragments.png)

1. 將最適化表單片段拖放至 **最適化表單片段** 最適化表單上的元件。

   >[!NOTE]
   >
   >未啟用最適化表單片段來從最適化表單內進行製作。 此外，您無法在JSON型最適化表單中使用XSD型片段，反之亦然。

最適化表單片段是參考最適化表單而新增，並與獨立的最適化表單片段保持同步。 這代表對最適化表單片段所做的任何修改，都會反映在片段併入最適化Forms的所有執行個體中。

### 在自適應表單中嵌入片段 {#embed-a-fragment-in-adaptive-form}

您可以選擇按一下「 」，將最適化表單片段嵌入最適化表單中。 ![內嵌](assets/Smock_Import_18_N.svg) 圖示新增片段的面板工具列

嵌入的片段不再與獨立片段連結。 您可以從最適化表單內編輯內嵌片段中的元件。

<!-- 
## Configure fragment appearance {#configure-fragment-appearance}

Any fragment you insert in Adaptive Forms appears as a placeholder image. The placeholder displays titles of up to a maximum of ten child panels in the fragment. You can configure AEM Forms to show the complete fragment instead of the placeholder image.

Perform the following steps to show complete fragments in forms:

1. Go to AEM web console configuration page at https:[*host*]:[*port*]/system/console/configMgr.

1. Search and click **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** to open it in edit mode.
1. Disable **[!UICONTROL Enable Placeholder in place of Fragment]** checkbox to show complete fragments rather than the placeholder image.

-->

### 在片段中使用片段 {#using-fragments-within-fragments}

您可以建立巢狀的Adaptive Form片段，這表示您可以將片段拖放到另一個片段中，而且可以有巢狀片段結構。



## 自動對應資料繫結的片段 {#auto-mapping-of-fragments-for-data-binding}

當您使用XFA表單範本或XSD複雜型別建立最適化表單片段，並將片段拖放至最適化表單時，XFA片段或XSD複雜型別會自動由對應的最適化表單片段取代，其片段模型根會對應至XFA片段或XSD複雜型別。

您可以從「編輯元件」對話方塊變更片段資產及其連結。

您也可以從AEM內容尋找器中的最適化表單片段資料庫拖放已繫結的最適化表單片段，並從Adaptive Form片段面板的「編輯」元件對話方塊提供正確的繫結參考。

## 管理片段 {#manage-fragments}

您可以使用AEM Forms UI對最適化表單片段執行數個操作。

1. 前往 `https://[hostname]/aem/forms.html`。

1. 按一下 **選取** 在AEM Forms UI工具列中選取最適化表單片段。 工具列會顯示您對選取的Adaptive Form片段可以執行的下列操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>說明</strong></p> </td>
  </tr>
  <tr>
   <td><p>編輯</p> </td>
   <td><p>在編輯模式中開啟選取的Adaptive Form片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>屬性</p> </td>
   <td><p>開啟屬性面板。 從「屬性」面板中，您可以檢視和編輯屬性、產生預覽，以及上傳所選片段的縮圖影像。 如需詳細資訊，請參閱 <a>管理中繼資料</a>.<br /> <br /> </p> </td>
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
   <td><p>提供通過將 XML 檔中的資料與片段合併來將片段預覽為 HTML 或自訂預覽的選項。 有關詳細資訊，請參閱 <a> 預覽表單 </a> 。 <br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>開始檢閱/管理檢閱</p> </td>
   <td><p>允許啟動和管理所選片段的審查。 如需詳細資訊，請參閱 <a>建立和管理稽核</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>新增字典</p> </td>
   <td><p>產生字典，用於當地語系化選取片段。 有關更多資訊，請參閱 <a> 當地語系化自我調整Forms </a> 。 <br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publish/取消發佈</p> </td>
   <td><p>發佈/取消發佈選取的片段。 <br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>刪除</p> </td>
   <td><p>刪除選取的片段。<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## 使用片段時要記住的關鍵點 {#key-points-to-remember-when-working-with-fragments}

* 確保片段名稱是唯一的。 如果存在具有相同名稱的現有片段，則片段無法建立。
* 在XDP型最適化表單中，如果您將面板儲存為包含其他XDP片段的片段，則產生的片段將自動與子XDP片段繫結。 如果是XSD型最適化表單，產生的片段將繫結至結構描述根。
* 當您建立最適化表單片段時，會建立片段節點，這類似於CRXDe Lite中最適化表單的guideContainer節點。
* 不支援使用不同表單資料模型的最適化表單中的片段。 例如，基於 XDP 的自我調整表單不支援基於 XDP 的片段，反之亦然。
* 您可透過 Finder 中的「最適化表單片段標籤AEM 內容使用最適化表單片段。
* 獨立自我調整表單片段中的任何運算式、腳本或樣式在通過引用插入或嵌入自我調整表單時都會保留。
* 您無法從最適化表單中編輯透過參考插入的最適化表單片段。 要進行編輯，您可以編輯獨立的最適化表單片段或將片段嵌入最適化表單中。
* 發佈最適化表單時，您需要發佈在最適化表單中透過參考插入的獨立最適化表單片段。
* 重新發佈更新的自我調整表單片段時，更改會反映在使用片段的最適化表單的已發佈實例中。
* 包含驗證元件的最適化表單不支援匿名使用者。 此外，不建議使用最適化表單片段中的驗證元件。
* （ **僅限** Mac）為了確保表單片段功能在所有場景中都能完美運行，請將以下內容添加到 /private/etc/hosts 檔中：
  `127.0.0.1 <Host machine>`**主機：** 部署AEM Forms的 Apple Mac 電腦。

## 參考片段 {#reference-fragments}

您可以使用參考最適化表單片段來建立您的表單。
<!-- For more information, see [Reference Fragments](../../forms/using/reference-adaptive-form-fragments.md). -->

## 另請參閱 {#see-also}

* [新增最適化表單至 AEM Sites 頁面或體驗片段](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [在最適化Forms中建立或新增主題](/help/forms/using-themes-in-core-components.md)
* [根據核心元件在AEM最適化表單中使用Google reCAPTCHA](/help/forms/captcha-adaptive-forms-core-components.md)
