---
title: 如何編輯或新增中繼資料
description: 透過 [!DNL Experience Manager Assets] 了解資產中繼資料的各種編輯資產中繼資料的方式。
contentOwner: AG
feature: 中繼資料
role: User,Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: 568c25d77eb42f7d5fd3c84d71333e083759712d
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 8%

---

# 如何編輯或新增中繼資料 {#how-to-edit-or-add-metadata}

中繼資料是可搜尋資產的其他相關資訊。 上傳影像時，會自動擷取它。 您可以編輯現有中繼資料，或將新中繼資料屬性新增至現有欄位（例如，中繼資料欄位空白時）。

由於公司需要可控且可靠的中繼資料辭匯，[!DNL Experience Manager Assets]不允許臨時新增新中繼資料屬性。 雖然作者無法為資產新增中繼資料欄位，但開發人員可以。 請參閱[為資產建立新中繼資料屬性](meta-edit.md#editing-metadata-schema)。

## 編輯資產的中繼資料 {#editing-metadata-for-an-asset}

若要編輯中繼資料：

1. 執行下列任一操作：

   * 從「資產」UI中，選取資產，然後按一下/點選工具列中的&#x200B;**[!UICONTROL 檢視屬性]**&#x200B;圖示。
   * 從資產縮圖中，選取&#x200B;**[!UICONTROL 檢視屬性]**&#x200B;快速動作。
   * 在資產頁面中，按一下/點選工具列中的「檢視屬性&#x200B;]**」。**[!UICONTROL 

   資產頁面會顯示資產的所有中繼資料。 此中繼資料上傳（擷取）至Experience Manager資產時會自動擷取。

1. 視需要對各種標籤下的中繼資料進行編輯，在完成時，按一下工具列中的「儲存 **** 」以儲存您所做的變更。按一下/點 **[!UICONTROL 選「關閉]** 」，返回「資產」網頁介面。

   >[!NOTE]
   >
   >如果文字欄位空白，則沒有現有的中繼資料集。 您可以在欄位中輸入值，並儲存它以新增該中繼資料屬性。

對資產中繼資料所做的任何變更，都會回寫至原始二進位檔，作為其XMP資料的一部分。 這是透過Experience Manager中繼資料回寫工作流程來完成。 對現有屬性所做的更改（如`dc:title`）將被覆蓋，新建立的屬性（包括`cq:tags`等自定義屬性）將與架構一起添加。

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## 編輯中繼資料結構 {#editing-metadata-schema}

有關如何編輯元資料架構的詳細資訊，請參閱[編輯元資料架構表單](metadata-schemas.md#edit-metadata-schema-forms)。

## 在Experience Manager中註冊自訂命名空間 {#registering-a-custom-namespace-within-aem}

您可以在Experience Manager中新增您自己的命名空間。 就像有預先定義的命名空間，例如cq、jcr和sling，您也可以擁有儲存庫中繼資料和xml處理的命名空間。

1. 前往節點類型管理頁面&#x200B;*https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*。
1. 按一下或點選頁面頂端的「**[!UICONTROL 命名空間]**」。 命名空間管理頁面會顯示在視窗中。

1. 若要新增命名空間，請按一下或點選底部的「**[!UICONTROL 新增]**」。
1. 在XML命名空間約定中指定自定義命名空間（以URI的形式指定ID以及該ID的相關前置詞），然後按一下或點選&#x200B;**[!UICONTROL Save]**。
