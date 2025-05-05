---
title: 瞭解通用編輯器
description: 本教學課程可協助您啟動並執行通用編輯器介面。 它會引導您瞭解使用者介面，以便在Universal Editor中建立您自己的Edge Delivery Services表單。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 0%

---


# 探索通用編輯器(WYSIWYG)介面

[Universal Editor](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)為Adobe Edge Delivery Services Forms提供簡單、視覺化且直覺式的What You See Is What You Get (WYSIWYG)介面。 它提供現代化的介面，具備拖放功能，有助於有效率地撰寫表單。

![通用編輯器使用者介面](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## 您將瞭解的內容

在本教學課程結束時，您將：

- 瞭解通用編輯器介面的主要元件
- 自信地瀏覽不同的介面區段
- 瞭解如何存取及使用必要的表單建立工具
- 熟悉可提高生產力的鍵盤快速鍵

## 瞭解通用編輯器介面

使用通用編輯器編輯表單時，主控台會開啟互動式WYSIWYG介面，讓您立即開始編輯。 此介面會在您工作時提供即時視覺化意見反應，向一般使用者顯示您表單的確切外觀。

>[!NOTE]
>
> 若要瞭解如何使用通用編輯器編寫表單，請參閱文章[使用通用編輯器(WYSIWYG)開始使用適用於AEM Forms的Edge Delivery Services ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)。

![通用編輯器使用者介面](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

Universal Editor介面分為四個邏輯部分：

- **[A： Experience Cloud標頭](#experience-cloud-header)**
- **[B：通用編輯器工具列](#universal-editor-toolbar)**
- **[C：屬性面板](#properties-panel)**
- **[D：編輯器](#editor)**

讓我們來詳細探索每個區段。

### Experience Cloud標題

Experience Cloud標題會顯示在主控台頂端，提供更廣泛的Adobe Experience Cloud生態系統內的導覽內容。 它會顯示您目前的位置，並可讓您快速存取其他Experience Cloud應用程式。

![Universal Editor Experience Cloud標題](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

讓我們檢查每個元件：

- **Adobe Experience Cloud**

  按一下畫面左側的&#x200B;**Adobe Experience Cloud**&#x200B;連結，可讓您導覽至Experience Manager解決方案的根目錄。 從那裡，您可以存取其他工具，例如Experience Manager Sites、Experience Manager Assets和Experience Manager Guides。

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png)

- **組織名稱**

  **組織名稱**&#x200B;會顯示您目前登入的Identity Management System (IMS)組織名稱。 如果您擁有多個組織的存取權，可以使用此下拉式選單在它們之間切換。 例如，在熒幕擷圖中，目前選取的IMS組織為「AEM Forms Internal01」。

  ![組織](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png)

- **說明**

  「說明」圖示可讓您快速存取學習與支援資源。 當您遇到挑戰或需要特定功能的指引時，這特別有用。 您也可以透過本節提交意見反應。

  ![說明](/help/edge/docs/forms/universal-editor/assets/ue-help.png)

- **通知**

  **通知**&#x200B;區段會顯示目前指派給您IMS組織中未完成通知、請求和目前工作的數量。 留意此區段有助於您隨時掌握工作流程。

  ![通知](/help/edge/docs/forms/universal-editor/assets/ue-notification.png)

- **解決方案**

  **解決方案**&#x200B;功能表可讓您切換至其他Adobe Experience Cloud解決方案，讓您在工作流程的不同工具之間輕鬆移動。

  ![解決方案](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png)

- **使用者設定檔**

  此圖示會顯示您的設定檔資訊，以及您目前登入的IMS組織名稱。 按一下此圖示可存取帳戶設定和登出選項。

  ![作者](/help/edge/docs/forms/universal-editor/assets/ue-author.png)

### 通用編輯器工具列

工具列提供基本的導覽與編輯工具。 有了它，您可以在表單之間移動、發佈或取消發佈表單、編輯表單屬性，以及存取規則編輯器以新增動態行為。

![通用編輯器工具列](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

以下是每個元件所提供的功能：

- **首頁按鈕**

  「首頁」按鈕可讓您回到「通用編輯器」的起始頁。 當您需要開始使用其他表單時，這個功能會很有用。 您也可以直接在位置列中輸入URL，以導覽至您要編輯的任何表單。

  ![通用編輯器首頁](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

- **位置列**

  **位置列**&#x200B;顯示您目前編輯的表單位址。 若要切換至其他表單，只要按一下位置列並輸入其URL即可。 焦點位置列的鍵盤快速鍵是`l`。

  ![位置列](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

- **規則編輯器**

  **規則編輯器**&#x200B;可讓您透過直覺式的視覺介面，將動態行為新增至表單。 使用它，您可以建立條件、驗證和動作來回應使用者的輸入，讓您的表單互動且聰明。

  ![規則編輯器](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > - 在Universal Editor中，預設不會啟用規則編輯器擴充功能。 若要啟用這項強大的功能，請從您的正式電子郵件地址透過[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)與我們連絡。
  > - 若要瞭解如何建立和管理規則，請參閱文章[WYSIWYG Authoring中的規則編輯器簡介](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md)。

- **編輯表單屬性**

  **編輯表單屬性**&#x200B;選項可讓您設定重要的表單設定，例如表單資料模型(FDM)和發佈日期。 這些屬性會影響表單的行為以及與後端系統的整合。

  ![編輯表單屬性](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

- **驗證標頭設定**

  **驗證標頭設定**&#x200B;選項可讓您設定本機開發目的的自訂驗證標頭。 在測試需要驗證憑證的表單時，此功能特別有用。

  ![驗證標頭](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

- **回應模式**

  **回應模式**&#x200B;功能可讓您測試您的表單在不同裝置上的顯示方式。 依預設，編輯器會在案頭版面中開啟，但您可以切換至行動檢視，以確保您的表單仍然可用，並且在較小的熒幕上吸引人。

  ![回應模式](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

- **預覽模式**

  **預覽模式**&#x200B;顯示您的表單與發佈時顯示的完全相同。 這可讓您按一下連結和按鈕來與表單互動，就像您的使用者一樣。 這是發佈前的重要步驟，可驗證一切都如預期般運作。 使用鍵盤快速鍵`p`在編輯和預覽模式之間切換。

  ![預覽](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

- **開啟頁面**

  **開啟頁面**&#x200B;按鈕會在新的瀏覽器標籤中開啟您的表單以供預覽。 這可提供不含編輯器介面的表單全熒幕檢視。 此動作的鍵盤快速鍵為`o`。

  ![開啟頁面](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

- **發佈**

  一旦您的表單可供使用者使用後，**發佈**&#x200B;按鈕就會讓表單上線，並且可供您的對象使用。 這是表單建立工作流程的最後一步。

  ![發佈](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

- **省略符號選單**

  按一下省略符號(...)會顯示其他選項，包括&#x200B;**取消發佈**&#x200B;目前上線的表單的功能。 當您需要暫時從公開存取中移除表單或將其取代為更新版本時，這會很有用。

  ![省略符號](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

### 屬性面板

**屬性面板**&#x200B;會顯示在介面的右側，並根據您在表單中選取的內容顯示內容相關資訊。 未選取任何元件時，會顯示整體表單結構。

![屬性面板](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

讓我們來探索其主要元件：

- **屬性模式**

  **屬性**&#x200B;模式會顯示您目前選取之元件的設定和選項。 您可以在此處自訂表單的個別元素，以符合特定需求。 開啟所選元件屬性的鍵盤快速鍵為`d`。

  ![屬性](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

- **內容樹狀結構**

  **內容樹狀結構**&#x200B;會顯示表單的階層結構。 此視覺化表示可協助您瞭解元件如何彼此巢狀化。 按一下樹狀結構中的任何專案時，會在編輯器中選取該專案並捲動至其位置。 這在複雜表單中特別有用。 使用鍵盤快速鍵`f`切換內容樹狀檢視。

  ![內容樹](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

- **產生變化版本**

  **產生變數**&#x200B;功能可運用人工智慧，根據特定提示建立不同的表單版本。 這可幫助您實驗不同的方法和設計，而無需手動建立每個變數。 提示可由Adobe提供或由您自訂。

  ![產生變化版本](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

  >[!NOTE]
  >
  > 如需使用表單產生變數的詳細指示，請參閱[產生變數](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)文章。

- **實驗中**

  **Experimentation**&#x200B;功能可讓您執行比較不同表單設計和配置的控制測試。 透過分析使用者與每個變體的互動方式，您可以進行資料導向式決策，以最佳化轉換率和使用者體驗。

  ![實驗中](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

- **Personalization**

  **Personalization**&#x200B;設定可讓您將表單與Adobe Experience Platform (AEP)或外部應用程式連線。 此連線可讓您根據使用者資料和行為建立量身打造的表單體驗，提高相關性和參與度。

  ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

- **A/B測試**

  **A/B測試**&#x200B;可協助您比較表單的特定變數，以判斷哪些變數表現更好。 不同於更廣泛的實驗，A/B測試通常會專注於比較特定元素或變更，以找出最有效的選項。

  ![A/B測試](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

- **任務管理**

  **工作管理**&#x200B;功能可協助您的團隊組織、追蹤及完成與表單建立和最佳化相關的工作，藉此簡化共同作業。 這能確保專案以明確責任的方式有效率地推進。

  ![任務管理](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

- **內容草稿**

  **Content Drafts**&#x200B;功能可讓您建立並儲存表單中文字元素的初步版本。 您可以使用現有的表單文字來建立草稿，或從頭開始，然後視需要編輯或刪除草稿。 依預設，您會看到三個草稿，但按一下「**全部顯示**」會顯示其他草稿。

  ![內容草稿](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

- **資料Source**

  **資料Source**&#x200B;選項可讓您設定並選取表單資料模型(FDM)的資料來源。 此整合可讓您所選來源的所有資料模型物件、屬性和服務都可在表單中使用，以啟用動態資料擷取和提交。

  ![資料Source](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

- **新增**

  「**新增**」按鈕會顯示可新增至目前所選容器的元件下拉式清單。 例如，選取最適化表單區段時，此清單會顯示可新增至該區段的所有元件。 開啟此元件清單的鍵盤快速鍵是`a`。

  ![新增圖示](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

- **重複**

  **複製**&#x200B;選項會建立您所選元件的完整復本。 這可在您需要多個類似元素時節省時間，因為您可以複製然後修改，而不是從頭開始建立。

  ![重複的圖示](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)

- **刪除**

  **刪除**&#x200B;選項會從您的表單移除選取的元件。 使用此選項時請務必小心，因為它會立即移除元素，而不會出現確認提示。

  ![刪除](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### 編輯者

編輯器是您建立和修改表單的中央工作區。 它會顯示位置列中指定的表單，並提供WYSIWYG體驗，向使用者顯示表單的確切外觀。 在預覽模式中，您可以像使用者一樣與表單互動，測試透過按鈕和連結的導覽。

![編輯器](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

編輯器是您花大部分時間、新增元件、設定其屬性並安排它們建立直覺式有效表單體驗的地方。

## 鍵盤快速鍵摘要

若要提高生產力，請記住這些重要的鍵盤快速鍵：

- `l` — 聚焦位置列
- `p` — 在編輯和預覽模式之間切換
- `o` — 在新索引標籤中開啟表單
- `d` — 開啟所選元件的屬性
- `f` — 切換內容樹狀結構檢視
- `a` — 開啟要新增的元件清單


