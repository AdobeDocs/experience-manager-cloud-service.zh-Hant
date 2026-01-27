---
title: 表單產生器：使用核心元件建立表單
description: 瞭解如何使用AEM Forms的表單產生器，以使用核心元件建立最適化表單。 適合需要回應式HTML5表單的表單建立者，這些表單可簡化資訊收集和處理。
keywords: 表單產生器，核心元件，建立表單，表單建立器，調適型表單，建立表單， AEM forms，回應式表單
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '2352'
ht-degree: 48%

---

# 表單產生器：使用核心元件建立表單 {#creating-an-adaptive-form-core-components}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-core-components/create-an-adaptive-form-core-components.html?lang=zh-Hant) |
| AEM as a Cloud Service  | 本文章 |


AEM Forms的表單產生器可讓您建立吸引人、回應式、動態且最適化的表單。 無論您是建立專業表單的表單建立者，還是需要快速建立回應式表單，AEM Forms都能提供使用者易用的精靈。 精靈具有快速索引標籤導覽，可輕鬆選取預先設定的範本、樣式、欄位和提交選項。

開始之前，請先了解您可以使用的表單元件類型：

* [最適化表單核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)：這些是標準化的資料擷取元件。這些元件會為您的數位註冊體驗提供自訂功能、縮短的開發時間，並降低維護成本。開發人員可以輕鬆地自訂這些元件和設計其樣式。Adobe建議使用這些現代且可擴展的元件來開發最適化Forms。

* [最適化表單基礎元件](creating-adaptive-form.md)：這些是經典 (舊) 的資料擷取元件。您可以繼續使用這些元件來編輯以現有基礎元件為主的最適化表單。如果您要建立新表單，Adobe建議使用[最適化Forms核心元件](creating-adaptive-form-core-components.md)來建立最適化Forms。

![建立最適化表單的精靈](/help/release-notes/assets/wizard.png)


## 必要條件

您必須符合以下條件才能建立最適化表單：



* **最適化表單範本**：此範本會提供基本結構並定義最適化表單的外觀 (版面和樣式)。其中具有包含特定屬性和內容結構的預先格式化元件。它也會提供定義主題和提交動作的選項。主題會定義外觀，而提交動作會定義提交最適化表單時要採取的動作。例如，將所收集的資料傳送到資料來源。雲端服務會提供一個名為 blank 的 OOTB 範本：

   * 該 `blank` 範本會包含在每個新的 AEM Forms as a Cloud Service 程式中。
   * 您可以透過套件管理員安裝參考套件，將該 `blank` 範本新增到您的 AEM Forms as a Cloud Service 程式。
   * 您也可以從頭開始[建立最適化Forms範本（核心元件）](/help/forms/template-editor-core-components.md)。
   * 您也可以將[範例範本](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=zh-Hant)部署至您的環境。 這些功能可協助您快速建立表格。

* **最適化表單主題**：主題包含元件和面板的樣式詳細資料。樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。套用主題時，指定的樣式會反映在對應的元件上。每個新的AEM Forms as a Cloud Service程式都會包含`Canvas`範本。 您也可以將[範例主題](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=zh-Hant)部署至您的環境。 這些可幫助您開始設計表單的樣式，並提供基礎結構，以根據您的業務需求建立或自訂主題。

  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create an Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **權限**：將您的使用者新增到 [!DNL forms-users] 群組。[!DNL forms-users] 群組的成員擁有建立最適化表單的權限。如需表單特定之使用者群組的詳細清單，請參閱[群組和權限](forms-groups-privileges-tasks.md)。

<!--
>[!NOTE]
>
>
> In addition to the given themes and templates when you enable Core Components, you can also deploy the latest out-of-the box [sample themes and templates](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html?lang=zh-Hant) to your AEM environment for use in Core Components based Adaptive Forms.
-->

## 建立最適化表單  {#create-an-adaptive-form-core-components}

1. 登入您的 [!DNL Experience Manager Forms] 作者執行個體；可以是 Cloud 執行個體或本機開發執行個體。

1. 在 Experience Manager 登入頁面上輸入您的認證。登入後，在左上角選取「**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表單]** > **[!UICONTROL 表單與文件]**」。

1. 選取「**[!UICONTROL 建立]**  > **[!UICONTROL 最適化表單]**」。此時會開啟精靈。在「來源」標籤中，選取一個範本：

   ![核心元件範本](/help/forms/assets/core-components-template.png)

   選取範本時，會自動選取範本中指定的主題和提交動作，且「**[!UICONTROL 建立]**」按鈕已啟用。您可以前往「**[!UICONTROL 樣式]**」或「**[!UICONTROL 提交]**」標籤，選取不同的主題或提交動作。如果選取的範本並未指定主題，則「建立」按鈕將維持停用狀態。您可以前往「**[!UICONTROL 樣式]**」標籤以手動選取主題。

   >[!NOTE]
   >
   >
   > 如果您的環境中沒有&#x200B;**最適化表單 (核心元件)** 範本，請[為您的環境啟用最適化表單核心元件](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project)。為您的環境啟用核心元件後，**最適化表單 (核心元件)** 範本就會新增到您的環境中。

1. 在「**[!UICONTROL 樣式]**」標籤中，選取一個主題：

   * 所選取的範本指定主題時，就會在精靈中自動選取該主題。您也可以從「樣式」標籤中選擇不同的主題。

   * 如果選取的範本未指定主題，您可以使用「樣式」標籤選擇主題。只有在選取主題之後，「**[!UICONTROL 建立]**」按鈕才會啟用。

1. (選用) 在「資料」標籤中，選取一個資料模型：

   * **表單資料模型(FDM)**： [表單資料模型](data-integration.md)可讓您將實體和服務從不同的資料來源整合到最適化表單。 如果您要建立的最適化表單涉及從多個資料來源擷取及寫入資料，請選擇表單資料模型(FDM)。

   * **JSON 結構描述**：[JSON 結構描述](adaptive-form-json-schema-form-model.md)是我們以核心元件為主的最適化表單，透過提供與 JSON 結構描述建立關聯的能力 (代表要產生或使用的資料結構)，可以與組織的後端系統緊密整合。這種關聯可讓作者使用結構描述的元素，動態地將內容新增到最適化表單。在編寫過程中，您可以在內容瀏覽器的資料模型物件標籤中輕鬆存取結構描述的元素，而且所有欄位都會自動新增到任何建立的調適型表單中。

   根據預設，系統會自動選取相關聯 JSON 結構描述的所有欄位，並轉換成對應的最適化表單元件，進而簡化編寫流程。該精靈提供額外的便利性，讓您透過核取方塊就能選擇性地選擇要在最適化表單中納入哪些欄位。

1. 在「**[!UICONTROL 提交]**」標籤中，選取提交動作：

   * 您選取範本後，系統會自動選取範本中指定的提交動作。您可以從「提交」標籤選取不同的提交動作。「**[!UICONTROL 提交]**」標籤會顯示所有可用的提交動作。

   * 所選取的範本未指定提交動作時，您可以使用「**[!UICONTROL 提交]**」標籤選取提交動作

1. (選用) 在「**[!UICONTROL 傳遞]**」標籤中，您可以為最適化表單指定發佈或取消發佈日期。

1. 選擇 **[!UICONTROL 建立]**。此時會顯示一個對話框，以指定標題、名稱和儲存最適化表單的位置：

   * **[!UICONTROL 標題：]**&#x200B;指定表單的顯示名稱。標題有助於在 [!DNL Experience Manager Forms] 使用者介面中識別表單。
   * **[!UICONTROL 名稱：]**&#x200B;指定表單的名稱。存放庫中會建立具有指定名稱的節點。您開始輸入標題時，就會自動產生名稱欄位的值。您可以變更建議的值。名稱欄位只能包含字母數字字元、連字號和底線。所有無效的輸入都會以連字號取代。
   * **[!UICONTROL 路徑：]**&#x200B;指定最適化表單的儲存位置。您可以將最適化表單直接儲存在 `/content/dam/formsanddocuments`，或建立一個資料夾 (例如 `/content/dam/formsanddocuments/adaptiveforms`) 以儲存最適化表單。要使用路徑中的資料夾之前，請務必先建立該資料夾。「**[!UICONTROL 路徑]**」欄位不會自動建立資料夾。

1. 選擇 **[!UICONTROL 建立]**。此時已建立最適化表單，並在最適化表單編輯器中開啟。編輯器會顯示範本中可用的內容。根據最適化表單的型別，相關<!--XFA form template, XML schema or --> JSON結構描述或表單資料模型(FDM)中存在的表單元素會顯示在側邊欄中&#x200B;**[!UICONTROL 內容瀏覽器]**&#x200B;的&#x200B;**[!UICONTROL 資料模型物件]**&#x200B;索引標籤中。 您也可以拖放這些元素以建置自己的最適化表單。

現在，您可以將[最適化Forms核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)拖放至最適化Forms容器來設計和建立表單。 您也可以造訪[https://aemcomponents.dev/](https://aemcomponents.dev/)，檢視作用中的可用核心元件。

>[!NOTE]
>
> 您也可以[使用XFA表單範本（*.XDP檔案）建立最適化Forms](/help/forms/create-adaptive-form-using-xfa-templates.md)。 它讓您透過直接在調適型Forms中重複使用XDP檔案的欄位來節省時間。

## 設定最適化表單的提交動作 {#configure-submit-action-for-form}

提交動作讓您可選擇透過最適化表單擷取的資料目標。當使用者按一下最適化表單上的提交按鈕時會觸發。 調適型表單包含一些立即可用的提交動作。 您也可以擴充預設提交動作，以建立自己的自訂提交動作。 若要設定表單的提交動作：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。

1. 按一下「**[!UICONTROL 提交]**」標籤。

   ![按一下扳手圖示可開啟「最適化表單容器」對話框，以設定提交動作](/help/forms/assets/adaptive-forms-submit-message.png)

1. 根據您的要求選取和設定「**[!UICONTROL 提交動作]**」。如需提交動作的詳細資訊，請參閱[最適化表單提交動作](/help/forms/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## 將使用者重新導向至頁面，或在提交表單時顯示感謝訊息

在提交表單時，您可以將使用者重新導向至其他網頁或訊息。 若要重新導向使用者或設定感謝訊息：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 開啟&#x200B;**[!UICONTROL 提交]**&#x200B;標籤。

   ![按一下扳手圖示以開啟最適化表單容器對話方塊，以設定重新導向頁面或感謝您的訊息](/help/forms/assets/adaptive-forms-redirect-message.png)

   * 若要設定重新導向URL，請在[送出]選項中選取&#x200B;**[!UICONTROL 重新導向至URL]**&#x200B;選項，然後瀏覽並選取AEM Sites頁面，或提供外部頁面的URL。

   * 若要設定自訂或感謝訊息，請在[送出]選項中選取&#x200B;**[!UICONTROL 顯示訊息]**&#x200B;選項，並在&#x200B;**[!UICONTROL 訊息內容]**&#x200B;方塊中提供訊息。 它是RTF文字方塊，您可以使用全熒幕選項來檢視所有可用的RTF專案。

## 為最適化表單設定結構描述或表單資料模型(FDM){#configure-schema-or-data-model-for-form}

您可以使用表單資料模型(FDM)將表單連線至資料Source，以根據使用者動作傳送及接收資料。 您也可以將表單連接至 JSON 結構描述，以預先定義的格式接收提交的資料。根據需求，將表單連線到JSON結構描述或表單資料模型(FDM)：

* [建立JSON結構描述並上傳至您的環境](/help/forms/adaptive-form-json-schema-form-model.md)
* [建立表單資料模型(FDM)](/help/forms/create-form-data-models.md)

### 為您的表單設定JSON結構描述或表單資料模型(FDM)

若要設定表單的JSON結構描述或表單資料模型(FDM)：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 開啟&#x200B;**[!UICONTROL 資料模型]**&#x200B;標籤。

   ![按一下「扳手」圖示以開啟「最適化表單容器」對話方塊，以設定JSON結構描述或表單資料模型(FDM)](/help/forms/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. 根據您的要求，選取並設定JSON結構描述或表單資料模型(FDM)：

   * 當您選取&#x200B;**[!UICONTROL 表單模型]**&#x200B;選項時，請使用&#x200B;**[!UICONTROL 選取表單資料模型]**&#x200B;選項來選取預先設定的表單資料模型(FDM)。
   * 當您選取&#x200B;**[!UICONTROL 結構描述]**&#x200B;選項時，請使用&#x200B;**[!UICONTROL 結構描述]**&#x200B;選項為您的表單選取JSON結構描述。

1. 按一下&#x200B;**[!UICONTROL 完成]**。

## 設定預填服務  {#configure-prefill-service-for-form}

您可以使用預填服務，使用現有資料自動填寫最適化表單的欄位。 當使用者開啟表單時，這些欄位的值將被預填。 您可以：

* [建立自訂預填服務](/help/forms/prepopulate-adaptive-form-fields.md)
* [使用表單資料模型預填服務](#fdm-prefill-service)

### 使用表單資料模型預填服務預先填入最適化表單的欄位 {#fdm-prefill-service}

您可以使用表單資料模型預填服務，透過表單資料模型或自訂預填服務預先填入最適化表單的欄位。 表單資料模型預填服務使用已設定的表單資料模型[的](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services)Get服務來擷取資料。 若要針對最適化表單使用表單資料模型預填服務：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下最適化表單容器屬性![最適化表單容器屬性](/help/forms/assets/configure-icon.svg)圖示。 用來設定資料模型的最適化表單容器對話方塊隨即開啟。
   ![按一下扳手圖示以開啟最適化表單容器對話方塊，以設定重新導向頁面或感謝您的訊息](/help/forms/assets/adaptive-forms-container-prefill-service.png)
1. 選取表單資料模型(FDM)。 開啟&#x200B;**[!UICONTROL 基本]**&#x200B;標籤。 在預填服務中，選取&#x200B;**[!UICONTROL 表單資料模型預填服務]**。
1. 按一下&#x200B;**[!UICONTROL 完成]**。 您的最適化表單現在已設定為使用表單資料模型預填。 您現在可以使用[規則編輯器](rule-editor.md)來建立規則以預先填入表單的欄位。

## 編輯最適化表單的表單模型屬性 {#edit-form-model}

1. 選取最適化表單，然後選取![頁面資訊](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL 開啟屬性]**。 此時會開啟「表單屬性」頁面。

1. 前往「**[!UICONTROL 表單模型]**」標籤並選擇表單模型。如果最適化表單沒有表單模型，您可以自由選擇JSON結構描述或表單資料模型(FDM)。 另一方面，如果最適化表單已經是以表單模型為主，您可以選擇切換到相同類型的另一個表單模型。例如，如果表單使用JSON架構，您可以輕鬆切換至其他JSON架構，同樣如果表單使用表單資料模型(FDM)，您可以切換至其他表單資料模型(FDM)。

1. 選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存屬性。


## 如何重新命名AEM最適化表單？ {#rename-an-AEM-Adaptive-Form}

若要重新命名最適化表單，請執行下列步驟：

1. 在您的AEM Forms使用者介面中選取最適化表單。
1. 按一下位於上方邊欄上的&#x200B;**屬性**。
1. 變更&#x200B;**標題**&#x200B;標籤中的表單名稱，如下圖所示。
1. 按一下「**儲存並關閉**」。

![重新命名AEM最適化表單](/help/forms/assets/change-af-name.png)



## 適用性和使用案例

### 保險

## AEM Forms是否可同時用於針對客戶的和內部的保險流程？

可以。AEM Forms支援客戶面對的數位表格，以及由內部、員工或代理程式主導的流程，例如稽核、核准和輔助資料擷取。

## AEM Forms是否可用於保險索賠提交？

可以。AEM Forms支援多步驟調適型表單，可讓保單持有人以數位方式提交保險索賠，包括擷取結構化資料及支援檔案。

## AEM Forms是否支援行動保險索賠？

可以。AEM Forms支援回應式且方便使用的表單，方便客戶和代理商從行動裝置提交保險資訊。
