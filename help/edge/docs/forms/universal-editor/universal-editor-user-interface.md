---
title: 瞭解Universal Editor — 開發人員教學課程
description: 本教學課程可協助您啟動並執行通用編輯器介面。 它會引導您瞭解使用者介面，以便在Universal Editor中建立您自己的Edge Delivery Services表單。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 2%

---

# 探索通用編輯器(WYSIWYG)介面

[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)為Adobe Edge Delivery Services (EDS) Forms提供簡單、視覺化且直覺式的What You See Is What You Get (WYSIWYG)介面。 它提供現代化的介面，具備拖放功能，有助於有效率地撰寫表單。

![通用編輯器使用者介面](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## 瞭解通用編輯器介面

當表單作者使用通用編輯器編輯表單時，主控台會開啟互動式WYSIWYG介面，讓使用者開始編輯表單。

>[!NOTE]
>
> 若要瞭解如何使用通用編輯器編寫表單，請參閱文章[使用通用編輯器(WYSIWYG)開始使用適用於AEM Forms的Edge Delivery Services ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)。

![通用編輯器使用者介面](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

Universal Editor介面分為四個部分：

* **[A： Experience Cloud標頭](#experience-cloud-header)**
* **[B：通用編輯器工具列](#universal-editor-toolbar)**
* **[C：屬性面板](#properties-panel)**
* **[D：編輯器](#editor)**

### Experience Cloud標題

Experience Cloud標題位於主控台頂端。 它會提供Experience Cloud中目前位置的相關資訊。 它也可讓您導覽至其他Experience Cloud應用程式。

![Universal Editor Experience Cloud標題](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)


讓我們瞭解它的每個元件。

* **Adobe Experience Cloud**

  您可以按一下畫面左側的&#x200B;**Adobe Experience Cloud**&#x200B;連結，導覽至Experience Manager解決方案的根目錄，並存取Experience Manager Sites、Experience Manager Assets和Experience Manager Guides之類的工具。

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png){width=50%，height=50%}

* **組織名稱**

  **組織名稱**&#x200B;會顯示您目前登入的IMS組織名稱。 您可以從下拉式清單中選取，切換至其他IMS組織（如果他們可存取其他組織）。 例如，目前選取的IMS組織名稱為`AEM Forms Internal01`。

  ![組織](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png){width=50%，height=50%}


* **說明**

  說明圖示可讓您快速存取學習與支援資源。 表單作者也可以在&#x200B;**說明**區段中新增意見回應。
  ![說明](/help/edge/docs/forms/universal-editor/assets/ue-help.png){width=50%，height=50%}


* **通知**

  **通知**&#x200B;區段顯示IMS組織中目前指派的未完成通知數、請求數以及目前任務數。

  ![通知](/help/edge/docs/forms/universal-editor/assets/ue-notification.png){width=50%，height=50%}


* **解決方案**

  您可以使用&#x200B;**解決方案**連結切換到其他Experience Cloud解決方案。
  ![解決方案](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png){width=50%，height=50%}


* **作者**
圖示代表表單作者的詳細資訊，以及作者目前登入的IMS組織名稱。
  ![作者](/help/edge/docs/forms/universal-editor/assets/ue-author.png){width=50%，height=50%}

### 通用編輯器工具列

工具列可讓您導覽至並編輯其他表單。 它也可讓使用者發佈或取消發佈表單、編輯表單屬性並存取規則編輯器。
![通用編輯器工具列](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

讓我們瞭解它的每個元件。

* **首頁按鈕**
首頁按鈕可讓您導覽至通用編輯器的起始頁面。 您也可以使用通用編輯器，直接輸入您要編輯之表單的URL。
  ![通用編輯器首頁](/help/edge/docs/forms/universal-editor/assets/ue-home.png)



* **位置列**
**位置列**&#x200B;顯示作者正在編輯的表單位址。 您也可以按一下位置列來輸入其他表單URL。 開啟位置列的捷徑鍵是鍵`l`。
  ![位置列](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png){width=50%，height=50%}



* **規則編輯器**

  **規則編輯器**&#x200B;提供直覺式的視覺介面，用於建立和管理規則。 您可以使用規則編輯器來新增動態表單行為。

  ![規則編輯器](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > * 在通用編輯器中，規則編輯器延伸模組預設為未啟用。若要啟用規則編輯器延伸模組，請從您的官方電子郵件 ID 寫信至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) 來和我們聯絡。
  > * 若要瞭解如何建立規則，請參閱文章[ WYSIWYG Authoring中的規則編輯器簡介](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)。

* **編輯表單屬性**
您可以按一下**編輯表單屬性**選項，以編輯表單屬性，例如表單資料模型和發佈日期。
  ![編輯表單屬性](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)



* **驗證標頭設定**
**驗證標頭設定**可讓作者設定自訂驗證標頭，以供本機開發之用。
  ![驗證標頭](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png){width=50%，height=50%}



* **回應模式**
  **回應式模式**&#x200B;選項可讓您定義通用編輯器如何呈現表單。 依預設，編輯器會在案頭版面配置中開啟，其中高度和寬度由瀏覽器自動決定。 或者，您可以選擇模擬行動裝置，並檢查表單在行動裝置上的顯示方式。

  ![回應式模式](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=50%，height=50%}


* **預覽模式**
在預覽模式中，表單會與發佈時完全顯示在編輯器中。 這可讓作者按一下連結和按鈕，以導覽表單。 在滿意編輯內容後，作者就可以為即時使用者發佈表單。 在編輯和預覽模式之間切換的捷徑鍵為`p`。
  ![預覽](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

* **開啟頁面**
**開啟頁面**&#x200B;選項會在新索引標籤中開啟表單以供預覽。 在新索引標籤中以預覽模式開啟表單的捷徑鍵是`o`。
  ![開啟頁面](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

* **發佈**

  您可以使用&#x200B;**發佈**按鈕讓即時使用者可以使用表單。
  ![發佈](/help/edge/docs/forms/universal-editor/assets/ue-publish.png){width=50%，height=50%}

* **省略符號**
當作者按一下(...)省略符號選項時，會出現**取消發佈**&#x200B;選項。 您可以使用&#x200B;**取消發佈**選項來取消發佈表單。
  ![省略符號](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png){width=50%，height=50%}

### 屬性面板

**屬性面板**位於編輯器的右側。 它會顯示表單階層中選取之元件的詳細資訊。 若未選取任何元件，則為預設結構。
![ue-properties面板](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png){width=50%，height=50%}


讓我們瞭解它的每個元件。


* **屬性模式**
在**Properties**&#x200B;選項中，會在編輯器中顯示所選元件的屬性。 例如，影像會顯示所選數字輸入元件的屬性。 您可以使用此選項修改元件的屬性。 開啟元件屬性的捷徑鍵是`d`。

  ![ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties.png){width=50%，height=50%}


* **內容樹狀結構**
**內容樹狀結構**&#x200B;選項會顯示表單的階層。 當作者按一下內容樹狀結構中的專案時，編輯器會選取該專案並捲動至該元件。 在內容樹狀檢視之間切換的捷徑鍵是鍵`f`。

  ![內容樹狀結構](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png){width=50%，height=50%}


* **產生變化版本**
  **產生變數**&#x200B;會使用人工智慧，根據特定提示產生不同版本的表單。 這些提示可由Adobe提供，或由表單作者製作和管理。

  ![變數](/help/edge/docs/forms/universal-editor/assets/ue-variations.png){width=50%，height=50%}


  >[!NOTE]
  >
  > 如需使用表單產生變數的指示，請參閱[產生變數](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)文章

* **實驗中**：

  **實驗性**是指用來測試各種不同的表單和版面配置以最佳化使用者體驗和效能的技術。
  ![實驗中](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png){width=50%，height=50%}


* **Personalization**
**Personalization**選項會設定設定，以在表單與Adobe Experience Platform (AEP) (屬於Adobe生態系統或外部應用程式的一部分)之間建立連線。
  ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png){width=50%，height=50%}


* **A/B測試**：
  **A/B測試**是指用來測試各種不同的表單和版面配置以最佳化使用者體驗和效能的技術。
  ![A/B測試](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png){width=50%，height=50%}



* **工作管理**：
**工作管理**功能可讓您簡化工作流程，並透過允許團隊管理、追蹤及執行與自訂及最佳化表單相關的工作，來增強共同作業
  ![工作管理](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png){width=50%，height=50%}

.
* **內容草稿**

  **Content Drafts**&#x200B;選項可讓您建立RTF元素的草稿。 您可以使用現有的表單文字或從頭開始建立草稿。 您可以視需要編輯或刪除草稿。 預設只會顯示三個草稿，但按一下「全部顯示」****&#x200B;會顯示其餘草稿。

  ![工作管理](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png){width=50%，height=50%}


* **資料Source**

  **資料Source**選項可讓您設定資料來源，並在建立表單資料模型(FDM)時選取資料來源。 它可讓所選資料來源的所有資料模型物件、屬性和服務都可用於表單資料模型。
  ![資料Source](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png){width=50%，height=50%}

* **新增**

  **新增**&#x200B;選項會開啟可新增至所選容器的元件下拉式清單。 例如，在最適化表單區段中，清單會顯示可新增至表單的可用元件。 開啟元件清單的捷徑鍵是`a`。
  ![新增圖示](/help/edge/docs/forms/universal-editor/assets/ue-add.png){width=50%，height=50%}

* **重複**

  **複製**選項會建立元件的復本，該元件是在內容樹狀結構或編輯器中選取的。
  ![重複的圖示](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png){width=50%，height=50%}


* **刪除**
**刪除**&#x200B;選項會刪除在內容樹狀結構或編輯器中選取的元件。

  ![刪除](/help/edge/docs/forms/universal-editor/assets/ue-delete.png){width=50%，height=50%}

### 編輯者

編輯器可讓您編輯表單，且在位置列中指定的表單會呈現在編輯區域中。 如果編輯器處於預覽模式，您可以使用可用的按鈕和連結來導覽表單。
![編輯器](/help/edge/docs/forms/universal-editor/assets/ue-editor.png){width=50%，height=50%}

## 另請參閱

{{universal-editor-see-also}}
