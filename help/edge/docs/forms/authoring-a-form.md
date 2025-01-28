---
Title: Authoring a Form
Description: This article provides information on various form authoring platforms, including the Universal Editor, document-based authoring, and Adaptive Forms editors (Core Components and Foundation Components).
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Adaptive Forms editors, Adaptive Forms editors for Core Components authoring, Adaptive Forms editors for Foundation Components authoring
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: ht
source-wordcount: '877'
ht-degree: 100%

---


# 編寫表單

Adobe Experience Manager 可提供並支援多個編輯器來編寫表單。您可以使用：
* 通用編輯器 (用於 WYSIWYG 編寫)
* Microsoft Excel 或 Google Sheets (稱為文件型編寫)
* 最適化表單編輯器 (用於核心元件或根據基礎元件的編寫)

**[要新增的影像]**

## 通用編輯器 (用於 WYSIWYG 編寫)

通用編輯器是多功能視覺化編輯器，可提供所見即所得 (WYSIWYG) 功能，確保直覺的表單建立體驗。建議在建立新表單時使用通用編輯器，因為它提供了新式、方便使用者的設計和便利的拖放介面。

若要使用通用編輯器建立表單，可使用 AEM 環境中提供的 Edge Delivery Services 範本。這些表單繼承了 Edge Delivery Services GitHub 存放庫中的設定的外觀和樣式。建立[AEM 環境與 Edge Delivery Services GitHub 存放庫之間的連線](/help/edge/docs/forms/publishing-forms.md)是為了在 Edge Delivery Services 上發佈這些表單。

如需有關如何使用通用編輯器進行編寫的詳細步驟，請參閱文件[「使用通用編輯器編寫內容」](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring)。

## Microsoft Excel 或 Google Sheets (稱為文件型編寫)

您可以使用文件型編寫透過 Microsoft Excel 或 Google Sheets 檔案來編寫表單，即可利用 Google Sheets、Microsoft Excel 和 Microsoft SharePoint 的強大生態系統和 API。這種方法對於在沒有進階提交服務的情況下建立簡單表單尤其實用。

若要開始使用 Microsoft Excel 或 Google Sheets 建立表單，請[使用 AEM Forms boilerplate 設定 AEM 專案](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)，並將對應的 GitHub 存放庫複製到本機。AEM Forms Edge Delivery 提供了稱為「最適化表單區塊」的功能，該功能可簡化建立用於擷取和儲存資料的表單的流程。若要了解如何使用 Edge Delivery Services 上的最適化表單區塊建立和發佈表單，請參閱[建立表單](/help/edge/docs/forms/create-forms.md)。

## 最適化表單編輯器 (用於核心元件或根據基礎元件的編寫)

您可以編寫引人入勝、反應靈敏且動態性的表單。最適化表單編輯器可提供方便使用者的精靈，讓您可以快速建立最適化表單。表單精靈具有簡單的索引標籤導覽功能，可讓您為基礎或核心元件、主題、資料模型和提交選項選取預先設定的範本，以有效率地建立表單。

[使用核心元件編寫表單](/help/forms/creating-adaptive-form-core-components.md)讓您可以利用可自訂的標準化資料擷取元件，從而縮減數位註冊體驗的開發時間並降低維護成本。這些表單可以使用 Edge Delivery Services 上的最適化表單區塊或透過 AEM Publish 執行個體進行發佈。

[使用 Foundation 元件編寫表單](/help/forms/create-an-adaptive-form.md)會使用經典的資料擷取元件。這些表單只能使用 AEM Publish 執行個體來發佈。

您也可以透過建立 [AEM 環境和 Edge Delivery Services GitHub 存放庫之間的連線](/help/edge/docs/forms/publishing-forms.md)來發佈使用 Edge Delivery Services 上的最適化表單編輯器所建立的表單。

## 如何在各種類型的表單編寫之間進行選擇？

下表會概述每個編寫編輯器的功能和使用案例，協助您根據您的需求和表單提交需求選擇合適的編輯器。

| **表單編寫編輯器** | **關鍵方法** | **功能** | **發佈方法** | **使用案例** |
|--------|-----------|-------|-------|------------------------------------------------|
| **文件型編寫** | 利用 Google Docs 和 Microsoft Office 等熟悉的工具來建立表單。 | 表單是使用試算表設計的，可和資料一起直接提交到 Google Sheets 或 Microsoft Excel 工作表。</br> </br> 這些表單的建立和部署速度更快。您無需具備任何 AEM 知識即可為這些表單開發自訂元件和樣式。 | 這些表單會發佈在 Edge Delivery Services 上，並具有非常高的 Google Lighthouse 分數。 </br> </br>  高分會帶來更快的渲染速度和更好的 SEO。 | 這些表單非常適合快速原型或不需要進階提交服務的基本表單。 </br> </br>  這些非常適合需要在試算表中儲存資料的調查、註冊或意見反應表單。這些表單會在 Edge Delivery services 上發佈 |
| **通用編輯器**  </br> </br> 如果您要建立新表單，請使用通用編輯器來建立表單。 | 提供 WYSIWYG 介面，用於直覺的表單建立。 | 表單是使用直覺的拖放介面設計的。</br> </br>  這些表單會借用對應表單已設定的 Edge Delivery Services GitHub 存放庫的外觀和樣式。 | 這些表單會發佈在 Edge Delivery Services 上，並具有非常高的 Google Lighthouse 分數。 </br> </br> 高分會帶來更快的渲染速度和更好的 SEO。 | 這些表單非常適合為 Edge Delivery Service 網站和頁面建立表單。這些表單案例需要複雜表單、複雜工作流程、自訂動作或與外部系統的整合 |
| **最適化表單編輯器** | 提供精靈驅動的方法，以使用範本、樣式和預先定義欄位快速開始表單編寫。 | 使用這些編輯器建立核心元件型表單或基礎元件型表單。 | 這些表單可以在 Edge Delivery Services 上或透過 AEM Publish 執行個體發佈。 | 使用這些編輯器建立核心元件型表單或基礎元件型表單。適於需要複雜表單、複雜工作流程、自訂動作或與外部系統整合的案例。 |


>[!NOTE]
>
>
> 如果您發現通用編輯器中缺少先前在最適化表單編輯器中可用的任何功能，您可以使用您的官方電子郵件地址寄送電子郵件至 mailto:aem-forms-ea@adobe.com 來要求這些功能。

## 相關文章

* [使用 Microsoft Excel 或 Google Sheets 的文件型編寫](/help/edge/docs/forms/create-forms.md)
* [通用編輯器或 WYSIWYG 編寫](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [建立最適化表單 (基礎元件)](/help/forms/creating-adaptive-form.md)
* [建立最適化表單 (核心元件)](/help/forms/create-an-adaptive-form.md)

## 另請參閱

{{see-more-forms-eds}}