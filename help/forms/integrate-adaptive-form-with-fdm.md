---
title: 如何將表單的表單資料模型(FDM)與最適化表單整合？
description: 了解如何根據表單資料模型 (FDM) 建立表單。產生並編輯 FDM 中資料模型物件的樣本資料。
feature: Edge Delivery Services, Adaptive Forms, Form Data Model
role: Admin, User
source-git-commit: 2c3e8f6f8dab1004a6fbd9be8f5604b1570a1808
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 27%

---

# 將表單與表單資料模型整合

將表單與表單資料模型(FDM)整合可讓您使用不同的後端資料來源來建立表單資料模型(FDM)。 您可以在不同的表單工作流程中，使用表單資料模型 (FDM) 作為綱要。設定資料來源並根據資料來源中可用的資料模型物件和服務建立表單資料模型 (FDM)。

## 將Forms與表單資料模型(FDM)整合的優點

* **順暢的後端連線**：不使用自訂程式碼將表單連線到各種後端系統(例如資料庫、REST API、SOAP服務、CRM)。 如此可即時交換資料並減少整合工作。
* **集中式資料結構描述**&#x200B;表單資料模型可作為統一的資料結構描述，可簡化跨多個表單和工作流程使用的資料物件與服務的對應和管理。

* **改善的表單預填和提交**：使用表單資料服務輕鬆設定預填和提交動作，確保精確且最新的資料擷取和儲存。

* **支援動態工作流程**：表單資料模型可與工作流程整合，以根據提交或擷取的資料自動化業務流程，提升整體效率。

## 先決條件

使用表單資料模型設定表單之前，請確定您已完成下列步驟：

* [設定資料來源](/help/forms/configure-data-sources.md)：設定資料來源，將表單連結至後端資料。
* [建立表單資料模型 (FDM)](/help/forms/create-form-data-models.md)：使用來自已設定的資料來源的資料物件和服務來建置資料模型。
* [設定資料模型物件與服務](/help/forms/work-with-form-data-model.md)：對應資料模型物件與服務，確保表單與資料來源間的資料能夠順利流通。

>[!BEGINTABS]

>[!TAB 基礎元件]

執行以下步驟，使用以基礎元件為基礎的最適化表單來設定表單資料模型，如下所示：

1. 開啟最適化表單以進行編輯，並導覽至最適化表單容器屬性的&#x200B;**[!UICONTROL 提交]**&#x200B;區段。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 使用表單資料模型提交]**。

   ![使用表單資料模型提交](/help/forms/assets/submit-uisng-fdm-fc.png)

1. 選取建立的&#x200B;**[!UICONTROL 資料模型以提交]**組態。
若要將附件提交至資料庫，請選取**提交表單附件**。 選取&#x200B;**提交記錄檔案**，記錄檔案(DoR)會儲存在資料庫中。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

>[!TAB 核心元件]

執行以下步驟，使用以核心元件為基礎的最適化表單來設定表單資料模型，如下所示：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下「**[!UICONTROL 提交]**」標籤。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[使用表單資料模型提交]**。
   ![使用表單資料模型提交](/help/forms/assets/submit-uisng-fdm-cc.png)

1. 選取建立的&#x200B;**[!UICONTROL 資料模型以提交]**組態。
若要將附件提交至資料庫，請選取**提交表單附件**。 選取&#x200B;**提交記錄檔案**，記錄檔案(DoR)會儲存在資料庫中。
1. 按一下「**[!UICONTROL 儲存]**」以儲存「提交」設定。

>[!TAB 通用編輯器]

執行以下步驟，以使用在Universal中編寫的最適化表單來設定表單資料模型，如下所示：

1. 開啟最適化表單進行編輯。
1. 按一下編輯器上的&#x200B;**編輯表單屬性**擴充功能。
**表單屬性**&#x200B;對話方塊就會顯示。

   >[!NOTE]
   >
   > * 如果您在通用編輯器介面中看不到&#x200B;**編輯表單屬性**&#x200B;圖示，請在Extension Manager中啟用&#x200B;**編輯表單屬性**&#x200B;擴充功能。
   > * 請參閱[Extension Manager功能焦點](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，瞭解如何在通用編輯器中啟用或停用擴充功能。
1. 按一下&#x200B;**提交**&#x200B;索引標籤，然後選取&#x200B;**[!UICONTROL 使用表單資料模型提交]**。
   ![OneDrive GIF](/help/forms/assets/submit-uisng-fdm-ue.png)
如果您選取**以原始名稱儲存附件**，則附件會使用其原始檔案名稱儲存在資料夾中。 您也可以將記錄檔案(DoR)儲存在Azure Blob儲存體中。
1. 選取您要儲存資料的「**[!UICONTROL 儲存空間設定]**」。
1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**

有關如何整合在通用編輯器中撰寫的表單的詳細說明，請參閱文章[將Forms與通用編輯器中的表單資料模型整合](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)。

>[!ENDTABS]

## 相關文章

{{af-submit-action}}
