---
Title: How Edge Delivery Services Forms work?
Description: This article provides information on how Edge Delivery Services Forms work. It also provides information on various form authoring platforms, including the Universal Editor and document-based authoring.
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Working of Edge Delivery Services Forms, How Edge Delivery Services Forms work?
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
exl-id: db58ce85-139a-4cc1-8e18-73da76357299
source-git-commit: bb01a76ae2bfd78ae648e91545f34f20fabebd10
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 100%

---


# Edge Delivery Services 表單

Adobe Edge Delivery Services 表單改造了編寫、執行和處理表單的方式。利用 Edge Delivery Services，組織即可建立快速、安全且高度可用的數位表單，並透過快速的開發環境增強使用者體驗和作業效率。透過 Edge Delivery Services Forms，您可以提高轉換率、降低成本並加速內容交付。

## Edge Delivery Services 表單的優勢

* **更快速建立表單**：使用完美的 Lighthouse 分數建立高效能表單，並使用真實使用者監控 (RUM) 持續監控其實際效能。

* **簡化的製作流程**：可輕鬆管理來自多個來源的內容，並實現更大的彈性。您即刻就可以使用 WYSIWYG 和文件型製作來建立表單，從而讓各種內容格式緊密整合。

* **非技術使用者可輕鬆上手**：使用 Edge Delivery Services 不需要廣泛的程式設計知識，因此非程式設計師也能輕鬆管理和發佈表單。

* **提升的使用者體驗**：可確保快速的載入時間和順暢的互動，因此可為使用者實現最短的等待時間和直覺式表單填寫體驗。

* **無伺服器執行**：Edge Delivery Services 可支援表單邏輯的無伺服器執行。其中包括：

   * **用戶端驗證**：表單欄位驗證會發生在用戶端，從而減少往返延遲。

   * **預先填入及個人化**：表單資料預先填入會在用戶端處理，以實現無縫的使用者體驗。

   * **提交處理**：表單提交會經過驗證並安全地轉寄，無需中央伺服器

## Edge Delivery Services 表單如何運作？

使用者可以使用 Google Drive、SharePoint 或通用編輯器 (WYSIWYG 製作) 等文件型製作工具來編寫 Edge Delivery Services 表單，同時可利用 GitHub 存放庫中可用的基本樣式、行為和元件。編寫完成後，Edge Delivery Services 表單即可使用表單提交服務將資料傳送到任何平台。

![Edge Delivery Services 表單如何運作](/help/edge/docs/forms/assets/eds-forms-working.png)

### Edge Delivery Service 表單的重要元件

Edge Delivery Servies 表單的重要元件包括：

* **GitHub 存放庫**：GitHub 存放庫可作為建立 Edge Delivery Services 表單的範本。這些表單會利用存放庫中的基本樣式和功能，並讓使用者可在 Edge Delivery Services 表單中新增自訂內容和自訂元件。

* **表單製作**：Edge Delivery Services 表單可支援兩種製作類型：WYSIWYG 和文件型製作。文件型製作讓使用者能夠使用 Google Docs 和 Microsoft Office 等熟悉的工具建立表單。WYSIWYG 製作則讓使用者可使用通用編輯器以視覺化方式設計表單，非技術使用者因此也可以輕鬆建立和管理表單。通用編輯器可提供直覺式表單建立體驗以及多種表單功能。

* **表單提交服務**：表單提交服務讓您可在任何平台上儲存表單所提交的資料，例如 OneDrive、SharePoint 或 Google Sheets 等平台，從而讓您輕鬆地在慣用系統中存取和管理表單資料。

## 編寫表單

Adobe Experience Manager 可提供並支援多個編輯器來編寫表單。您可以使用：
* [通用編輯器 (用於 WYSIWYG 編寫)](#universal-editor-for-wysiwyg-authoring)
* [Microsoft Excel 或 Google Sheets (稱為文件型編寫)](#microsoft-excel-or-google-sheets-known-as-document-based-authoring)

### 通用編輯器 (用於 WYSIWYG 編寫)

通用編輯器是多功能視覺化編輯器，可提供所見即所得 (WYSIWYG) 功能，確保直覺的表單建立體驗。建議在建立新表單時使用通用編輯器，因為它提供了新式、方便使用者的設計和便利的拖放介面。

若要使用通用編輯器建立表單，可使用 AEM 環境中提供的 Edge Delivery Services 範本。這些表單繼承了 Edge Delivery Services GitHub 存放庫中的設定的外觀和樣式。建立[AEM 環境與 Edge Delivery Services GitHub 存放庫之間的連線](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)是為了在 Edge Delivery Services 上發佈這些表單。

如需有關如何使用通用編輯器進行編寫的詳細步驟，請參閱文件[「使用通用編輯器編寫內容」](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring)。

### Microsoft Excel 或 Google Sheets (稱為文件型編寫)

您可以使用文件型編寫透過 Microsoft Excel 或 Google Sheets 檔案來編寫表單，即可利用 Google Sheets、Microsoft Excel 和 Microsoft SharePoint 的強大生態系統和 API。這種方法對於在沒有進階提交服務的情況下建立簡單表單尤其實用。

若要開始使用 Microsoft Excel 或 Google Sheets 建立表單，請[使用 AEM Forms boilerplate 設定 AEM 專案](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)，並將對應的 GitHub 存放庫複製到本機。AEM Forms Edge Delivery 提供了稱為「最適化表單區塊」的功能，該功能可簡化建立用於擷取和儲存資料的表單的流程。若要了解如何使用 Edge Delivery Services 上的最適化表單區塊建立和發佈表單，請參閱[建立表單](/help/edge/docs/forms/create-forms.md)。

<!--
## Adaptive Forms editors (for Core Components or foundation components based authoring)

You can author forms that are engaging, responsive and dynamic. The Adaptive Form editor provides a user-friendly wizard that allows you to quickly create Adaptive Forms. The form wizard features easy tab navigation, enabling you to select pre-configured templates for foundation or core components, themes, data models, and submission options to create a form efficiently. 

[Authoring forms with Core Components](/help/forms/creating-adaptive-form-core-components.md) allows you to leverage standardized data capture components that can be customized, reducing development time and lowering maintenance costs for digital enrollment experiences. These forms can be published using the Adaptive Forms Block on Edge Delivery Services or through the AEM Publish instance. 

[Authoring forms with Foundation Components](/help/forms/create-an-adaptive-form.md) uses classic data capture components. These forms can only be published using the AEM Publish instance. 

You can also publish forms created using Adaptive Forms Editors on Edge Delivery Services by establishing [connection between your AEM environment and the Edge Delivery Services GitHub repository](/help/edge/docs/forms/publishing-forms.md).


| **Adaptive Forms editors** | Provides a wizard-driven approach to quickly start forms authoring using templates, styling, and predefined fields. | Use these editors to create Core Components based forms or Foundation Components based forms. | These forms can be published on Edge Delivery Services or via AEM Publish instances.  | Use these editors to create Core Components based forms or Foundation Components based forms. Ideal for scenarios involving complex forms, complex workflows, custom actions, or integrations with external systems. |  



## Types of Publishing for Edge Delivery Services Forms

You can publish Edge Delivery Services Forms on one of the following:

* **Edge Delivery Services Form Submission**: Edge Delivery Services Form Submissions ensure that form interactions, including submission and data processing, are handled efficiently and securely. This enables a faster and more reliable user experience, particularly during high traffic periods. By processing form submissions at the edge, Edge Delivery Services minimizes the reliance on a centralized server.

* **AEM Publish instance**: The AEM Forms server offers a publish instance that manages the forms and related assets available to end users.
-->

### 如何在各種類型的表單編寫之間進行選擇？

下表會概述每個編寫編輯器的功能和使用案例，協助您根據您的需求和表單提交需求選擇合適的編輯器。

| **表單編寫編輯器** | **關鍵方法** | **功能** | **發佈方法** | **使用案例** |
|--------|-----------|-------|-------|------------------------------------------------|
| **文件型編寫** | 利用 Google Docs 和 Microsoft Office 等熟悉的工具來建立表單。 | 表單是使用試算表設計的，可和資料一起直接提交到 Google Sheets 或 Microsoft Excel 工作表。</br> </br> 這些表單的建立和部署速度更快。您無需具備任何 AEM 知識即可為這些表單開發自訂元件和樣式。 | 這些表單會發佈在 Edge Delivery Services 上，並具有非常高的 Google Lighthouse 分數。 </br> </br>  高分會帶來更快的渲染速度和更好的 SEO。 | 這些表單非常適合快速原型或不需要進階提交服務的基本表單。 </br> </br>  這些非常適合需要在試算表中儲存資料的調查、註冊或意見反應表單。這些表單會在 Edge Delivery services 上發佈 |
| **通用編輯器**  </br> </br> 如果您要建立新表單，請使用通用編輯器來建立表單。 | 提供 WYSIWYG 介面，用於直覺的表單建立。 | 表單是使用直覺的拖放介面設計的。</br> </br>  這些表單會借用對應表單已設定的 Edge Delivery Services GitHub 存放庫的外觀和樣式。 | 這些表單會發佈在 Edge Delivery Services 上，並具有非常高的 Google Lighthouse 分數。 </br> </br> 高分會帶來更快的渲染速度和更好的 SEO。 | 這些表單非常適合為 Edge Delivery Service 網站和頁面建立表單。這些表單案例需要複雜表單、複雜工作流程、自訂動作或與外部系統的整合 |

>[!NOTE]
>
>
> 如果您發現通用編輯器中缺少先前在最適化表單編輯器中可用的任何功能，您可以使用您的官方電子郵件地址寄送電子郵件至 mailto:aem-forms-ea@adobe.com 來要求這些功能。

## 另請參閱

{{see-more-forms-eds}}
