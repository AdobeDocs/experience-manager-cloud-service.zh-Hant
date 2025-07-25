---
title: 在通用編輯器中如何整合表單的表單資料模型 (FDM)？
description: 了解如何根據表單資料模型 (FDM) 建立表單。產生並編輯 FDM 中資料模型物件的樣本資料。
feature: Edge Delivery Services, Form Data Model
role: Admin, User
exl-id: 9ce51223-57d0-47d8-8868-84b37d4e8e3e
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: ht
source-wordcount: '1271'
ht-degree: 100%

---

# 在通用編輯器中整合表單與表單資料模型

在通用編輯器中整合表單與表單資料模型 (FDM)，讓您可以使用不同的後端資料來源來建立表單資料模型 (FDM)。您可以在不同的表單工作流程中，使用表單資料模型 (FDM) 作為綱要。設定資料來源並根據資料來源中可用的資料模型物件和服務建立表單資料模型 (FDM)。

## 考量事項

* 如果您在通用編輯器介面中沒有看到「**資料來源**」圖示，或在右側屬性面板中沒有看到「**繫結參考**」屬性，請在 **Extension Manager** 中啟用&#x200B;**資料來源**&#x200B;擴充功能。

  ![通用編輯器 Extension Manager 介面的螢幕擷圖顯示可用的擴充功能，包括為了表單整合而啟用的資料來源擴充功能](/help/edge/docs/forms/universal-editor/assets/extension-manager.png)

  請參閱[Extension Manager 功能重點介紹](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，了解如何在通用編輯器中啟用和停用擴充功能。

* 通用編輯器目前不支援表單預填服務。

## 先決條件

在通用編輯器中使用表單資料模型設定表單前，請確保您已完成下列步驟：

* [設定資料來源](/help/forms/configure-data-sources.md)：設定資料來源，將表單連結至後端資料。
* [建立表單資料模型 (FDM)](/help/forms/create-form-data-models.md)：使用來自已設定的資料來源的資料物件和服務來建置資料模型。
* [設定資料模型物件與服務](/help/forms/work-with-form-data-model.md)：對應資料模型物件與服務，確保表單與資料來源間的資料能夠順利流通。

## 在通用編輯器中使用表單資料模型建立表單

在通用編輯器中，您可以建立：

* [綱要型表單](#schema-based-form)：綱要型表單使用在「**資料**」標籤中建立表單時所設定的資料來源，自動將資料繫結至表單欄位。
* [非綱要型表單](#non-schema-based-form)：您必須手動新增非綱要型表單的資料來源，並從內容樹繫結每個欄位。

![通用編輯器中的表單類型](/help/edge/docs/forms/universal-editor/assets/form-types.png){width="50%" align="center" height="50%"}

您可以根據需求靈活運用這些方法，將資料模型連結至表單。

### 綱要型表單

建立綱要型表單時，系統會自動設定資料來源，並透過資料繫結將表單欄位連結至資料。如要使用表單建立精靈建立綱要型表單，請執行下列步驟：

1. 登入您的 [!DNL Experience Manager Forms] 作者實例。
1. 在 Experience Manager 登入頁面上輸入您的認證。登入後，在左上角選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。
1. 選取「**[!UICONTROL 建立]**  > **[!UICONTROL 最適化表單]**」。此時會開啟精靈。在「**來源**」標籤中，選取一個範本：

   ![Edge Delivery Services 範本](/help/edge/assets/create-eds-forms.png)

   當您選取 Edge Delivery Services 的範本時，便會啟用「**[!UICONTROL 建立]**」按鈕。您可以前往「**[!UICONTROL 資料來源]**」或「**[!UICONTROL 提交]**」標籤來選取資料來源或提交動作。

1. 在「**資料**」標籤中，您可以選取以下其中一種資料模型：

   * **表單資料模型 (FDM)**：將來自資料來源的資料模型物件和服務整合至您的表單中。若您的表單需要從多個來源讀取和寫入資料，請選擇表單資料模型 (FDM)。

   * **JSON 綱要**：透過與定義資料結構的 JSON 綱要建立關聯，將表單與後端系統整合。整合後您便能使用綱要元素新增動態內容。

     例如，選取一個已建立且命名為「寵物表單資料模型」的表單資料模型。

     ![選取表單資料模型](/help/edge/docs/forms/universal-editor/assets/select-petstore-form-data-model.png)


     根據預設，系統會自動選取相關聯 JSON 綱要或表單資料模型 (FDM) 的所有欄位，並轉換成對應的表單元件，進而簡化製作流程。此精靈亦提供核取方塊，讓您能自由選擇表單中要包含的欄位。

1. 按一下「**[!UICONTROL 建立]**」，便會出現「**建立表單**」精靈。
1. 設定「**名稱**」和「**標題**」。
1. 指定 **GitHub URL**。例如，若您的 GitHub 存放庫名稱為 `edsforms`、位於帳戶 `wkndforms` 之下，則 URL 為：
   `https://github.com/wkndforms/edsforms`
1. 按一下「**[!UICONTROL 建立]**」。

   ![建立綱要型表單](/help/edge/docs/forms/universal-editor/assets/create-schema-based-form.png)

   按一下「**[!UICONTROL 建立]**」後，便會在通用編輯器中開啟表單供您製作。

   ![通用編輯器的螢幕擷圖顯示一份綱要型表單，內含預先填入的表單欄位，且內容瀏覽器顯示可用的資料來源元素](/help/edge/docs/forms/universal-editor/assets/schema-based-form-in-ue.png)

   使用取自相關聯資料來源的資料元素來建立此表單，且表單欄位已預先設定資料繫結。

   ![自動資料繫結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   您現在能為表單新增及[設定提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)。

### 非綱要型表單

建立非綱要型表單時，系統不會設定任何資料來源。您可以稍後再編輯表單屬性來新增資料來源並手動設定表單欄位的資料繫結。執行下列步驟以編輯表單屬性並新增資料來源：

1. 登入您的 [!DNL Experience Manager Forms] 作者實例。
1. 在 Experience Manager 登入頁面上輸入您的認證。登入後，在左上角選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。
1. 選取要新增資料來源的表單，接著按一下「**[!UICONTROL 屬性]**」。
   ![開啟表單屬性](/help/edge/docs/forms/universal-editor/assets/non-schema-based-edit-properties.png)

   接著開啟了表單屬性。
1. 按一下開啟「**表單模型**」標籤，接著「在&#x200B;**選取表單**」下拉式選單中，您可以選取下列其中一個選項：

   * **表單資料模型 (FDM)**：使用表單資料模型建立表單。
   * **連接器**：使用 Adobe Marketo 資料來源建立表單。
   * **綱要**：使用上傳至 AEM Forms 的 JSON 綱要建立表單。
   * **無模型**：不使用任何表單模型，從頭開始建立表單。

     例如，選取表單資料模型 (FDM)

     ![選取表單模型標籤](/help/edge/docs/forms/universal-editor/assets/select-form-model.png)

1. 從下拉式選單中選取已建立的表單資料模型 (FDM)。例如，從下拉式選單中選擇已建立且命名為「寵物表單資料模型」的表單資料模型。

   ![選取 FDM](/help/edge/docs/forms/universal-editor/assets/select-fdm.png)

   選取表單資料模型 (FDM) 時，會出現警告對話框。按一下「**確定**」來關閉對話框。

   ![表單模型精靈](/help/edge/docs/forms/universal-editor/assets/form-model-wizard.png)

1. 按一下「**[!UICONTROL 儲存並關閉]**」。
1. 開啟表單進行編輯。表單會在通用編輯器中開啟以供製作。

   ![非綱要型表單製作](/help/edge/docs/forms/universal-editor/assets/non-schema-form-authoring.png)

   關聯表單資料模型 (FDM) 中的表單元素將會顯示在「**屬性面板**」中「**[!UICONTROL 內容瀏覽器]**」的「**[!UICONTROL 資料來源]**」標籤中。

   ![表單資料來源](/help/edge/docs/forms/universal-editor/assets/non-schema-data-source.png)

1. 從「**[!UICONTROL 資料來源]**」標籤中選取資料元素，接著按一下「**[!UICONTROL 新增]**」。

   ![新增資料元素](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-element.png)

   您也可以拖放這些元素以建置自己的最適化表單。按一下「**[!UICONTROL 新增]**」後，「**[!UICONTROL 資料來源]**」標籤中選取的元素將會新增至您的表單中，而且新增元素前面會顯示勾選符號。

   ![螢幕擷圖顯示通用編輯器正在將資料元素從「資料來源」索引標籤拖放到表單結構中，以建置非綱要型表單](/help/edge/docs/forms/universal-editor/assets/non-schema-form.png)

您從「**繫結參考**」屬性中選取資料繫結，即可把資料繫結新增至表單欄位。例如，我們對表單中已存在的文字方塊「**ID**」新增資料繫結參考：
若要從資料來源樹中選取表單欄位的資料繫結，請執行下列步驟：

1. 開啟要新增資料繫結參考的表單欄位屬性。
1. 前往「**繫結參考**」屬性，然後按一下「**瀏覽**」圖示。

   ![手動新增表單欄位的資料繫結](/help/edge/docs/forms/universal-editor/assets/non-schema-add-data-binding.png)

1. 從「**選取繫結參考**」精靈中的資料來源樹，選擇資料繫結參考。

   ![選取資料繫結參考](/help/edge/docs/forms/universal-editor/assets/select-bind-reference.png)

1. 從資料來源樹中選取要繫結至表單欄位的資料元素，然後按一下「**選取**」。

   ![選取資料元素](/help/edge/docs/forms/universal-editor/assets/select-data-element.png)

   該表單欄位繫結至資料元素，並顯示在「**繫結參考**」屬性中。

   ![自動資料繫結](/help/edge/docs/forms/universal-editor/assets/schema-based-form-data-binding.png)

   您也可以手動編輯表單欄位的「**繫結參考**」屬性。

您現在能為表單新增及[設定提交動作](/help/edge/docs/forms/universal-editor/submit-action.md)。

## 另請參閱

{{universal-editor-see-also}}
