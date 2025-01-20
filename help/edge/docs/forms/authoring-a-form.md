---
Title: Authoring a Form
Description: This article provides information on various form authoring platforms, including the Universal Editor, document-based authoring, and Adaptive Forms editors (Core Components and Foundation Components).
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Adaptive Forms editors, Adaptive Forms editors for Core Components authoring, Adaptive Forms editors for Foundation Components authoring
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 0%

---


# 製作表單

Adobe Experience Manager提供並支援多個編輯器以撰寫表單。 您可以使用：
* 通用編輯器(用於WYSIWYG編寫)
* Microsoft Excel或Google工作表（稱為檔案式製作）
* 最適化Forms編輯器（適用於核心元件或基礎元件的製作）

**[要新增的影像]**

## 通用編輯器(用於WYSIWYG編寫)

通用編輯器是一款多功能的視覺編輯器，提供隨心所欲的(WYSIWYG)功能，能確保建立直覺式的表單體驗。 建議在建立新表單時使用通用編輯器，因為它提供現代、好用的設計和便利的拖放介面。

若要使用通用編輯器建立表單，系統會使用AEM環境中可用的Edge Delivery Services範本。 這些表單的外觀會繼承自Edge Delivery ServicesGitHub存放庫中的設定。 [您的AEM環境與Edge Delivery Services GitHub存放庫之間建立連線](/help/edge/docs/forms/publishing-forms.md)，以便在Edge Delivery Services上發佈這些表單。

有關如何使用通用編輯器編寫的詳細步驟，請參閱[使用通用編輯器編寫內容](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring)文章。

## Microsoft Excel或Google工作表（稱為檔案式製作）

您可以使用檔案式製作結合Microsoft Excel或Google Sheets檔案來製作表單，讓您運用Google Sheets、Microsoft Excel和Microsoft SharePoint強大的生態系統和API。 這種方法對於建立沒有進階提交服務的簡單表單特別有用。

若要使用Microsoft Excel或Google Sheets開始建立表單，[請使用AEM Forms範本設定AEM專案](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block)，並將對應的GitHub存放庫複製到本機電腦。 AEM Forms Edge Delivery提供最適化Forms區塊功能，可簡化建立表單以擷取及儲存資料的程式。 若要瞭解如何在Edge Delivery Services上使用最適化Forms區塊來建立和發佈表單，請參閱[建立表單](/help/edge/docs/forms/create-forms.md)。

## 最適化Forms編輯器（適用於核心元件或基礎元件的製作）

您可以撰寫吸引人、回應式且動態的表單。 最適化表單編輯器提供使用者易記的精靈，可讓您快速建立最適化Forms。 表單精靈提供簡單的標籤導覽，讓您能夠選取基礎或核心元件、主題、資料模型和提交選項的預先設定範本，以有效建立表單。

[使用核心元件製作表單](/help/forms/creating-adaptive-form-core-components.md)可讓您運用可自訂的標準化資料擷取元件，減少開發時間並降低數位註冊體驗的維護成本。 這些表單可在Edge Delivery Services上使用Adaptive Forms區塊或透過AEM Publish例項發佈。

[使用Foundation元件編寫表單](/help/forms/create-an-adaptive-form.md)使用傳統資料擷取元件。 這些表單只能使用AEM Publish例項發佈。

您也可以在您的AEM環境與Edge Delivery ServicesGitHub存放庫](/help/edge/docs/forms/publishing-forms.md)之間建立[連線，以在Edge Delivery Services上發佈使用最適化Forms編輯器建立的表單。

## 如何在各種型別的表單製作之間進行選擇？

下表概述每個編寫編輯器的功能和使用案例，協助您根據需求和表單提交需求選擇正確的編輯器。

| **表單編寫編輯器** | **金鑰方法** | **功能** | **發佈方法** | **使用案例** |
|--------|-----------|-------|-------|------------------------------------------------|
| **文件型製作** | 利用熟悉的工具(例如Google Docs和Microsoft Office)建立表單。 | Forms的設計使用試算表，其資料會直接提交至Google工作表或Microsoft Excel工作表。</br> </br>這些表單的建立和部署速度更快。 您不需要預先瞭解AEM，即可為這些表單開發自訂元件和樣式。 | 這些表單發佈在Edge Delivery Services上，並擁有非常高的Google Lighthouse分數。</br> </br>高分數可加快轉譯速度並改善SEO。 | 這些表單適用於快速原型製作或不需要進階提交服務的基本表單。</br> </br>這些非常適合需要以試算表儲存資料的調查、註冊或意見回饋表單。 這些表單發佈在Edge Delivery服務上 |
| **通用編輯器** </br> </br>如果您要建立新表單，請使用通用編輯器建立表單。 | 提供WYSIWYG介面，用於建立直覺式表單。 | Forms的設計使用直覺式的拖放介面。</br> </br>這些表單會從已設定的Edge Delivery Services GitHub存放庫借用對應表單的外觀。 | 這些表單發佈在Edge Delivery Services上，並擁有非常高的Google Lighthouse分數。</br> </br>高分數可加快轉譯速度並改善SEO。 | 這些表單適用於建立Edge Delivery服務網站和頁面的表單。 這些表單情境涉及複雜表單、複雜工作流程、自訂動作或與外部系統的整合 |
| **最適化Forms編輯器** | 提供精靈導向的方法，以使用範本、樣式和預先定義的欄位快速開始表單撰寫。 | 使用這些編輯器建立以核心元件為基礎的表單或基礎元件為基礎的表單。 | 這些表單可發佈在Edge Delivery Services上或透過AEM Publish執行個體。 | 使用這些編輯器建立以核心元件為基礎的表單或基礎元件為基礎的表單。 適用於涉及複雜表單、複雜工作流程、自訂動作或與外部系統整合的情境。 |


>[!NOTE]
>
>
> 如果您發現通用編輯器中遺漏了先前在最適化Forms編輯器中提供的任何功能，您可以使用官方電子郵件地址來寄送電子郵件至mailto:aem-forms-ea@adobe.com以請求這些功能。

## 相關文章

* [使用Microsoft Excel或Google Sheets的檔案式撰寫](/help/edge/docs/forms/create-forms.md)
* 用於WYSIWYG製作的[通用編輯器](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [建立最適化表單（基礎元件）](/help/forms/creating-adaptive-form.md)
* [建立最適化表單（核心元件）](/help/forms/create-an-adaptive-form.md)

## 另請參閱

{{see-more-forms-eds}}