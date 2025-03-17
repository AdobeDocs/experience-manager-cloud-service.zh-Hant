---
title: 如何在Universal Editor中為表單建立表單資料模型(FDM)？
description: 瞭解如何根據表單資料模型(FDM)建立表單。 產生並編輯FDM中資料模型物件的範例資料。
feature: Edge Delivery Services, Form Data Model
role: Admin, User
hide: true
hidefromtoc: true
source-git-commit: e2259e542df5a12748705af901d073e4486292c4
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 5%

---


# 將表單與通用編輯器中的表單資料模型整合

在Universal Editor中整合表單與表單資料模型(FDM)，可讓您使用不同的後端資料來源來建立表單資料模型(FDM)。 您可以使用表單資料模型(FDM)作為各種表單工作流程中的結構描述。 根據資料來源中可用的資料模型物件和服務，設定資料來源並建立表單資料模型(FDM)。

## 考量

* 目前不支援通用編輯器中表單的預填服務。

## 先決條件

在Universal Editor中使用表單資料模型設定表單之前，請確定您已完成下列步驟：

* [設定資料Source](/help/forms/configure-data-sources.md)：設定資料來源，將您的表單連線到後端資料。
* [建立表單資料模型(FDM)](/help/forms/create-form-data-models.md)：使用來自已設定資料來源的資料物件和服務來建立資料模型。
* [設定資料模型物件及服務](/help/forms/work-with-form-data-model.md)：對應資料模型物件及服務，以確保表單與資料來源之間的資料流動順暢。

## 在Universal Editor中使用表單資料模型建立Forms

在Universal Editor中，您可以建立：
* [結構描述型表單](#schema-based-form)：結構描述型表單使用在&#x200B;**資料**&#x200B;索引標籤中表單建立期間設定的資料來源，自動將資料繫結至表單欄位。
* [非結構描述型表單](#non-schema-based-form)：非結構描述型表單需要您手動新增資料來源，並從內容樹狀結構繫結每個欄位。

通用編輯器中的![表單型別](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

這些方法可讓您根據自己的需求，靈活地將資料模型與表單連線。

### 以結構描述為基礎的表單

當您建立以結構描述為基礎的表單時，會自動設定資料來源，而表單欄位已透過資料繫結連結至資料。 若要使用「表單建立精靈」建立以結構描述為基礎的表單，請執行下列步驟：

1. 登入您的[!DNL Experience Manager Forms]作者執行個體。
2. 在 Experience Manager 登入頁面上輸入您的認證。登入後，在左上角選取&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]**。
3. 選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 最適化Forms]**。 此時會開啟精靈。在&#x200B;**Source**&#x200B;索引標籤中，選取範本：

   ![Edge Delivery Services範本](/help/edge/assets/create-eds-forms.png)

   當您選取以Edge Delivery Services為基礎的範本時，會啟用&#x200B;**[!UICONTROL 建立]**&#x200B;按鈕。 您可以前往&#x200B;**[!UICONTROL 資料Source]**&#x200B;或&#x200B;**[!UICONTROL 提交]**&#x200B;標籤，以選取資料來源或提交動作。

4. 在&#x200B;**資料**&#x200B;標籤中，您可以選取下列其中一個資料模型：

   * **表單資料模型(FDM)**：將資料來源中的資料模型物件和服務整合到您的表單中。 如果您的表單需要從多個來源讀取和寫入資料，請選擇「表單資料模型(FDM)」。

   * **JSON結構描述**：關聯定義資料結構的JSON結構描述，將您的表單與後端系統整合。 它可讓您使用結構元素來新增動態內容。

     例如，選取已建立的表單資料模型（名為Pet Form Data Model）。

     ![選取表單資料模型](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)


     依預設，系統會自動選取相關JSON結構描述或表單資料模型(FDM)的所有欄位，並將其轉換為對應的表單元件，進而簡化編寫程式。 精靈也可讓您使用核取方塊選擇性地選擇要包含在表單中的欄位。

5. 按一下&#x200B;**[!UICONTROL 建立]**，即會出現&#x200B;**建立表單**&#x200B;精靈。
6. 指定&#x200B;**名稱**&#x200B;和&#x200B;**標題**。
7. 指定 **GitHub URL**。例如，如果您的GitHub存放庫名為`edsforms`，則位於帳戶`wkndforms`下，URL為：
   `https://github.com/wkndforms/edsforms`
8. 按一下&#x200B;**[!UICONTROL 建立]**。

   ![建立結構描述型表單](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

   您按一下&#x200B;**[!UICONTROL 建立]**，表單即會在通用編輯器中開啟以供編寫。

   ![編寫表單](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

   表單是使用關聯資料來源的資料元素所建立，且表單欄位具有預先設定的資料繫結。

   ![自動資料繫結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   您現在可以為表單新增並[設定提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)。

### 非結構描述型表單

當您建立非結構描述型表單時，不會設定資料來源， 您可以稍後編輯表單屬性，以新增資料來源及手動設定表單欄位的資料繫結。 執行以下步驟來編輯表單屬性並新增資料來源：

1. 登入您的[!DNL Experience Manager Forms]作者執行個體。
1. 在 Experience Manager 登入頁面上輸入您的認證。登入後，在左上角選取&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]**。
1. 選取您要新增資料來源的表單，然後按一下&#x200B;**[!UICONTROL 屬性]**。
   ![開啟表單屬性](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

   表單屬性隨即開啟。
1. 按一下以開啟&#x200B;**表單模型**&#x200B;標籤，然後從&#x200B;**選取自**&#x200B;下拉式功能表。 您可以選取下列其中一個選項：

   * **表單資料模型(FDM)**：使用表單資料模型建立表單。
   * **聯結器**：使用Adobe Marketo資料來源建立表單。
   * **結構描述**：使用上傳至AEM Forms的JSON結構描述建立表單。
   * **無**：從頭開始建立表單，而不使用任何表單模型。

     例如，選取表單資料模型(FDM)

     ![選取表單模型索引標籤](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

1. 從下拉式清單中選取已建立的表單資料模型(FDM)。 例如，從下拉式清單中選取已建立的名為Pet Form Data Model的表單資料模型。

   ![選取FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

   選取「表單資料模型」(FDM)時，會出現警告對話方塊。 按一下&#x200B;**確定**&#x200B;關閉對話方塊。

   ![表單模型精靈](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

1. 按一下「**[!UICONTROL 儲存並關閉]**」。
1. 開啟表單進行編輯。 表單會在Universal Editor中開啟以進行編寫。

   ![非結構描述型表單製作](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

   關聯表單資料模型(FDM)中的表單元素會顯示在&#x200B;**屬性面板**&#x200B;中&#x200B;**[!UICONTROL 內容瀏覽器]**&#x200B;的&#x200B;**[!UICONTROL 資料來源]**&#x200B;索引標籤中。

   ![表單資料Source](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

1. 從&#x200B;**[!UICONTROL 資料來源]**&#x200B;索引標籤中選取資料元素，然後按一下&#x200B;**[!UICONTROL 新增]**。

   ![新增資料元素](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   您也可以拖放這些元素來建置最適化表單。 當您按一下&#x200B;**[!UICONTROL 新增]**，從&#x200B;**[!UICONTROL 資料來源]**&#x200B;索引標籤選取的元素會新增至您的表單，新增的元素前面會出現一個勾號。

   ![建置表單](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

   您也可以在表單元素的&#x200B;**繫結參考**屬性中指定資料繫結，以手動方式將資料繫結新增至表單元素。
例如，我們將資料繫結參考新增至表單中已存在的**Pet名稱**&#x200B;文字方塊：

   ![手動為表單欄位新增資料](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

   您現在可以為表單新增並[設定提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)。

## 另請參閱

{{universal-editor-see-also}}
