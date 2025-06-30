---
title: 如何編輯或新增中繼資料
description: 瞭解 [!DNL Experience Manager Assets] 中的資產中繼資料，以及編輯資產中繼資料的各種方式。
contentOwner: AG
feature: Metadata
role: User, Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 9%

---

# 如何編輯或新增中繼資料 {#how-to-edit-or-add-metadata}

中繼資料是可搜尋資產的其他相關資訊。 上傳影像時，系統會自動擷取該影像。 您可以編輯現有的中繼資料，或將新的中繼資料屬性新增到現有欄位（例如，當中繼資料欄位為空白時）。

由於公司需要受控且可靠的中繼資料辭彙，[!DNL Experience Manager Assets]不允許隨選新增新的中繼資料屬性。 雖然作者無法為資產新增中繼資料欄位，但開發人員可以。 請參閱[建立Assets的新中繼資料屬性](meta-edit.md#editing-metadata-schema)。

## 編輯資產的中繼資料 {#editing-metadata-for-an-asset}

若要編輯中繼資料：

1. 執行下列任一項作業：

   * 從Assets UI中選取資產，然後從工具列選取&#x200B;**[!UICONTROL 檢視屬性]**&#x200B;圖示。
   * 從資產縮圖中，選取&#x200B;**[!UICONTROL 檢視屬性]**&#x200B;快速動作。
   * 在資產頁面中，從工具列選取&#x200B;**[!UICONTROL 檢視屬性]**。

   資產頁面會顯示資產的中繼資料。 此中繼資料上傳（擷取）至Experience Manager Assets時，會自動擷取。

1. 視需要對各種標籤下的中繼資料進行編輯，在完成時，從工具列選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存您的變更。 選取&#x200B;**[!UICONTROL 關閉]**&#x200B;以返回Assets網頁介面。

   >[!NOTE]
   >
   >如果文字欄位為空，則沒有現有的中繼資料集。 您可以在欄位中輸入值，並將其儲存以新增該中繼資料屬性。

對資產中繼資料所做的任何變更，都會當作其XMP資料的一部分，回寫至原始二進位檔。 這可透過Experience Manager中繼資料回寫工作流程完成。 對現有屬性（例如`dc:title`）所做的變更會被覆寫，而建立的屬性（包括自訂屬性，例如`cq:tags`）會與結構描述一起新增。

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## 編輯中繼資料結構 {#editing-metadata-schema}

如需有關如何編輯中繼資料結構描述的詳細資訊，請參閱[編輯中繼資料結構描述表單](metadata-schemas.md#edit-metadata-schema-forms)。

## 在Experience Manager中註冊自訂名稱空間 {#registering-a-custom-namespace-within-aem}

您可以在Experience Manager中新增自己的名稱空間。 就像cq、jcr和sling等預先定義的名稱空間一樣，您可以擁有用於存放庫中繼資料和xml處理的名稱空間。

1. 前往節點型別管理頁面&#x200B;*https://&lt;host>：&lt;port>/crx/explorer/nodetypes/index.jsp*。
1. 選取頁面頂端的&#x200B;**[!UICONTROL 名稱空間]**。 名稱空間管理頁面會顯示在視窗中。

1. 若要新增名稱空間，請選取底部的&#x200B;**[!UICONTROL 新增]**。
1. 以XML名稱空間慣例指定自訂名稱空間（以URI格式指定ID，並為該ID指定相關的前置詞），然後選取&#x200B;**[!UICONTROL 儲存]**。

**另請參閱**

* [翻譯資產](translate-assets.md)
* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
