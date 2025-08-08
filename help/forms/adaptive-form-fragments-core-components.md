---
title: 什麼是自適應表單片段？
description: 最適化Forms提供一種機制，可建立在任何最適化表單中使用的表單區段（例如面板或欄位群組）。 您也可以將現有面板儲存為片段。
topic-tags: author
keywords: 新增最適化表單片段、最適化表單片段、建立表單片段、新增片段至最適化表單、管理片段
feature: Adaptive Forms, Core Components
exl-id: 3a9ad1b7-2f6f-4ca9-a1c9-549c4238c59e
role: User, Developer
source-git-commit: bc422429d4a57bbbf89b7af2283b537a1f516ab5
workflow-type: tm+mt
source-wordcount: '1479'
ht-degree: 10%

---

# 根據核心元件在最適化表單中建立和使用最適化Forms片段 {#adaptive-form-fragments}


| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service （核心元件） | 本文章 |
| AEM as a Cloud Service （基礎元件） | [按一下這裡](/help/forms/adaptive-form-fragments.md) |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/adaptive-form-fragments.html?lang=zh-Hant) |

雖然每個表單都是為特定目的而設計，但大多數表單中都有一些常見的區段，例如提供個人詳細資訊，例如姓名和地址、家庭詳細資訊、收入詳細資訊。 每次建立新表單時，表單開發人員都必須建立這些通用區段。

最適化Forms提供一種便利的機制，讓您只需建立一次表單區段（例如面板或欄位群組），即可在最適化Forms中重複使用。 這些可重複使用的獨立區段稱為「最適化表單片段」。

表單片段可無縫整合至多種表單，精簡建立一致且專業外觀的表單。 表單片段透過「一次變更，處處反映」功能確保可重複性、標準化和品牌一致性。由於在一處進行的更新會自動傳播到使用這些片段的所有表單，因此可體驗更高的可維護性和效率。

您可以將片段多次新增到檔案，並使用其元件的資料繫結屬性將其連結到不同的資料來源或結構描述。 例如，您可以將相同的地址片段用於永久、通訊和帳單地址，並將其連線到資料來源或結構的不同欄位。

>[!NOTE]
>
> 您可以使用[表單片段元件](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/adaptive-form-fragment)的「設定」對話方塊和「設計」對話方塊，輕鬆自訂使用者的片段體驗。

## 建立自適應表單片段 {#create-a-fragment}

您可以從頭開始建立最適化表單片段，或將現有最適化表單中的面板儲存為片段。 若要建立表單片段：

1. 在https://[*主機名稱*]：[*連線埠*]/aem/forms.html登入您的AEM Forms執行個體。
1. 按一下「**建立 > 自適應表單片段**」。

   ![建立最適化表單片段](/help/forms/assets/adaptive-form-fragment.png)

1. 指定片段的標題、名稱、說明和標籤。 確保為片段指定唯一的名稱。如果已存在名稱相同的片段，將無法建立片段。
1. 選取表單範本。 您可以為以核心元件為基礎的Adaptive Forms或基礎元件為基礎的Adaptive Forms建立表單片段。 若要建立核心元件型表單的表單片段，請選取核心元件型範本。

   當您建立核心元件型表單的表單片段時，請使用選取表單主題選項來選取核心元件型主題。

1. 按一下以開啟&#x200B;**表單模型**&#x200B;標籤，然後從&#x200B;**選取自**&#x200B;下拉式功能表中，為片段選取下列其中一個模型：

   ![在「表單模型」標籤中顯示模型類型](assets/create-af-1-1.png)

   * **無模型**：指定此選項，即可不使用任何表單模型，從頭開始建立表單。

     >[!NOTE]
     >
     > 在Adaptive Forms中，您可以使用單一表單片段（根據核心元件）多次。 它支援無型和結構描述型表單片段。

   * **結構描述**：指定使用上傳至AEM Forms的XML或JSON結構描述建立片段。 您可以上傳或從可用的XML或JSON結構描述中選取作為片段的表單模型。 選取XML結構描述時，您也可以從&#x200B;**[!UICONTROL XML結構描述複雜型別]**&#x200B;下拉式方塊中選取所選結構描述中存在的complexType，以建立最適化表單片段。 選取JSON結構描述時，您也可以從&#x200B;**[!UICONTROL JSON結構描述定義]**&#x200B;下拉式方塊中選取所選結構描述中存在的結構描述定義，以建立調適型表單片段。
   * **表單資料模型**：指定使用表單資料模型(FDM)建立片段。 您可以僅根據表單資料模型(FDM)中的一個資料模型物件來建立最適化表單片段。 展開表單資料模型(FDM)定義下拉式清單。 它會列出指定表單資料模型(FDM)中的所有資料模型物件。 從清單中選取資料模型物件。

   ![表單資料模型(FDM)](assets/create-af-3.png)

1. 按一下[建立]&#x200B;**&#x200B;**，然後按一下[開啟]&#x200B;**&#x200B;**，以編輯模式開啟具有預設範本的片段。 在編輯模式中，您可以將任何最適化表單元件新增到片段。

<!-- For information about Adaptive Form components, see [Introduction to authoring Adaptive Forms](../../forms/using/introduction-forms-authoring.md). --> 此外，如果您選取XML結構描述作為片段的表單模型，則內容尋找器中會顯示一個顯示表單模型階層的新索引標籤。 它可讓您將表單模型元素拖放至片段上。<!--The added form-model elements get converted into form components while retaining the original properties from the associated XDP or XSD. -->

根據結構描述或表單資料模型(FDM)的自適應表單片段建立後，表單資料模型(FDM)或結構描述元素會顯示在自適應表單編輯器中，內容瀏覽器的「資料來源」標籤中。 您可以將表單模型元素拖放至片段上。 新增的表單模型元素會轉換為表單元件，同時保留關聯結構描述的原始屬性。


## 將片段新增至最適化表單 {#insert-a-fragment-in-an-adaptive-form}

若要將最適化表單片段新增至最適化表單：

1. 在編輯模式中開啟最適化表單。
1. 將&#x200B;**最適化表單片段**&#x200B;元件新增至表單。
1. 開啟&#x200B;**最適化表單片段**&#x200B;元件的[設定]對話方塊。
1. 在「**基本**」標籤中，選取「**片段參考**」。您的表單可用的所有Adaptive Forms片段（視表單的模型而定）都會出現。

1. 選擇一個Adaptive Form片段到您的Adaptive Form上的&#x200B;**Adaptive Form Fragment**&#x200B;元件上。

   ![選取最適化表單片段選項](/help/forms/assets/adaptive-form-fragment-basic.png)

<!-- 
   >[!NOTE]
   >
   >The Adaptive Form fragment is not enabled for authoring from within the Adaptive Form. Moreover, you cannot use an XSD-based fragment in a JSON-based Adaptive Form and the opposite way. 
-->

最適化表單片段是參考最適化表單而新增，並與獨立的最適化表單片段保持同步。 這代表對最適化表單片段所做的任何修改，都會反映在片段併入最適化Forms的所有執行個體中。

<!--### Embed a fragment in Adaptive Form {#embed-a-fragment-in-adaptive-form}

You can choose to embed an Adaptive Form fragment in an Adaptive Form by clicking the ![Embed](assets/Smock_Import_18_N.svg) icon the panel toolbar of the added fragment

The embedded fragment is no longer linked with the standalone fragment. You can edit the components in the embedded fragment from within the Adaptive Form.-->

<!-- 
## Configure fragment appearance {#configure-fragment-appearance}

Any fragment you insert in Adaptive Forms appears as a placeholder image. The placeholder displays titles of up to a maximum of ten child panels in the fragment. You can configure AEM Forms to show the complete fragment instead of the placeholder image.

Perform the following steps to show complete fragments in forms:

1. Go to AEM web console configuration page at https:[*host*]:[*port*]/system/console/configMgr.

1. Search and click **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** to open it in edit mode.
1. Disable **[!UICONTROL Enable Placeholder in place of Fragment]** checkbox to show complete fragments rather than the placeholder image.

-->

### 在片段中使用片段 {#using-fragments-within-fragments}

您可以建立巢狀Adaptive Form片段，這表示您可以在另一個片段中新增片段，而且可以有巢狀片段結構。

### 在最適化表單中多次使用表單片段 {#using-form-fragment-mutiple-times-in-af}

您可以在調適型表單中多次使用無基礎和結構描述型表單片段，以唯一儲存每個表單片段欄位的資料。 例如，您可以使用地址表單片段來收集地址詳細資訊，以便永久性、通訊和在貸款申請表中呈現有效地址。

![在最適化表單中使用多個片段](/help/forms/assets/using-multiple-fragment-af.gif)

## 對最適化表單中的片段提供自動對應支援

當您根據JSON結構描述定義建立最適化表單片段時，它可以在從相同結構描述建立的表單中自動重複使用。
如果您拖放符合最適化表單片段JSON結構描述定義對應的結構描述物件或任何巢狀物件，物件會被相符的自適應表單片段取代。 此表單不會新增具有個別欄位的面板，而是插入對應的最適化表單片段。

![拖放片段](/help/forms/assets/fragment.png)

您也可以從AEM內容尋找器中的最適化表單片段資料庫拖放已繫結的最適化表單片段，並從Adaptive Form片段面板的「編輯」元件對話方塊提供正確的繫結參考。

## 管理片段 {#manage-fragments}

您可以使用AEM Forms UI對最適化表單片段執行數個操作。

1. 前往 `https://[hostname]/aem/forms.html`。

1. 按一下AEM Forms UI工具列中的&#x200B;**選取**，然後選取最適化表單片段。 工具列會顯示您對選取的Adaptive Form片段可以執行的下列操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>編輯</p> </td>
   <td><p>在編輯模式中開啟選取的最適化表單片段。<br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>預覽</p> </td>
   <td><p>提供以HTML預覽片段的選項，或透過合併XML檔案中的資料與片段來自訂預覽。 如需詳細資訊，請參閱<a>預覽表單</a>。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>下載</p> </td>
   <td><p>下載所選片段。<br /><br /> </p> </td>
  </tr>
  <tr>
   <td><p>開始評論/管理評論</p> </td>
   <td><p>允許啟動和管理所選片段的審查。 如需詳細資訊，請參閱<a>建立和管理評論</a>。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>新增字典</p> </td>
   <td><p>產生字典以將選取的片段本地化。 如需詳細資訊，請參閱<a>本地化最適化Forms</a>。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>發佈/取消發佈</p> </td>
   <td><p>發佈/取消發佈所選片段。<br /><br /> </p> </td>
  </tr>
  <tr>
   <td><p>刪除</p> </td>
   <td><p>刪除所選片段。<br /><br /> </p> </td>
  </tr>
 </tbody>
</table>

## 使用片段時要記住的關鍵點 {#key-points-to-remember-when-working-with-fragments}

* 確認片段使用唯一的名稱。如果現有片段擁有相同的名稱，則無法建立片段。
* 透過參考插入或嵌入自適應表單時，獨立自適應表單片段中的任何運算式、指令碼或樣式都會保留。
* 您無法從最適化表單中編輯透過參考插入的最適化表單片段。 若要編輯，請修改獨立的最適化表單片段。
* 發佈最適化表單時，您需要發佈在最適化表單中透過參考插入的獨立最適化表單片段。
* 當您重新發佈更新的Adaptive Form片段時，變更會反映在使用片段的Adaptive Form的已發佈例項中。
* 包含Verify元件的調適型表單不支援匿名使用者。 此外，不建議在自適應表單片段中使用驗證元件。

## 參考片段 {#reference-fragments}

您可以使用參考最適化表單片段來建立您的表單。
<!-- For more information, see [Reference Fragments](../../forms/using/reference-adaptive-form-fragments.md). -->



## 另請參閱 {#see-also}

{{see-also}}