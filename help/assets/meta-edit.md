---
title: 如何編輯或新增中繼資料
description: 了解中的資產中繼資料 [!DNL Experience Manager Assets] 編輯資產中繼資料的各種方式。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 9%

---

# 如何編輯或新增中繼資料 {#how-to-edit-or-add-metadata}

中繼資料是可搜尋資產的其他相關資訊。 上傳影像時，會自動擷取它。 您可以編輯現有中繼資料，或將新中繼資料屬性新增至現有欄位（例如，中繼資料欄位空白時）。

因為公司需要受控和可靠的元資料辭匯， [!DNL Experience Manager Assets] 不允許臨機新增中繼資料屬性。 雖然作者無法為資產新增中繼資料欄位，但開發人員可以。 請參閱 [為資產建立新的中繼資料屬性](meta-edit.md#editing-metadata-schema).

## 編輯資產的中繼資料 {#editing-metadata-for-an-asset}

若要編輯中繼資料：

1. 執行下列任一項作業：

   * 從「資產」UI中，選取資產，然後按一下/點選 **[!UICONTROL 檢視屬性]** 圖示。
   * 從資產縮圖中選取 **[!UICONTROL 檢視屬性]** 快速動作。
   * 從資產頁面，按一下/點選 **[!UICONTROL 檢視屬性]** 的上界。

   資產頁面會顯示資產的所有中繼資料。 此中繼資料上傳（擷取）至Experience Manager Assets時會自動擷取。

1. 視需要對各種標籤下的中繼資料進行編輯，在完成時，按一下工具列中的「儲存 **** 」以儲存您所做的變更。按一下/點 **[!UICONTROL 選「關閉]** 」，返回「資產」網頁介面。

   >[!NOTE]
   >
   >如果文字欄位空白，則沒有現有的中繼資料集。 您可以在欄位中輸入值，並儲存它以新增該中繼資料屬性。

對資產中繼資料所做的任何變更，都會回寫至原始二進位檔，作為其XMP資料的一部分。 這是透過Experience Manager中繼資料回寫工作流程來完成。 對現有屬性所做的變更(例如 `dc:title`)覆寫和新建立的屬性(包括自訂屬性，如 `cq:tags`)會與結構一起新增。

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## 編輯中繼資料結構 {#editing-metadata-schema}

如需如何編輯中繼資料結構的詳細資訊，請參閱 [編輯中繼資料結構表單](metadata-schemas.md#edit-metadata-schema-forms).

## 在Experience Manager中註冊自訂命名空間 {#registering-a-custom-namespace-within-aem}

您可以在Experience Manager中新增您自己的命名空間。 就像有預先定義的命名空間，例如cq、jcr和sling，您也可以擁有儲存庫中繼資料和xml處理的命名空間。

1. 轉至節點類型管理頁 *https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*.
1. 按一下或點選 **[!UICONTROL 命名空間]** 頁面頂端。 命名空間管理頁面會顯示在視窗中。

1. 若要新增命名空間，請按一下或點選 **[!UICONTROL 新增]** 在底部。
1. 在XML命名空間約定中指定自定義命名空間（以URI的形式指定ID以及ID的關聯前置詞），然後按一下或點選 **[!UICONTROL 儲存]**.
