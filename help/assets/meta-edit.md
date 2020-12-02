---
title: 如何編輯或新增中繼資料
description: 瞭解AEM Assets中的資產中繼資料，以及編輯資產中繼資料的各種方式。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 7%

---


# 如何編輯或新增中繼資料{#how-to-edit-or-add-metadata}

中繼資料是可搜尋之資產的其他資訊。 上傳影像時會自動擷取。 您可以編輯現有的中繼資料，或將新的中繼資料屬性新增至現有欄位（例如，中繼資料欄位空白時）。

由於公司需要可控且可靠的中繼資料辭彙，AEM Assets不允許臨機新增中繼資料屬性。 雖然作者無法為資產新增中繼資料欄位，但開發人員可以。 請參閱[建立資產的新中繼資料屬性](meta-edit.md#editing-metadata-schema)。

## 編輯資產{#editing-metadata-for-an-asset}的中繼資料

若要編輯中繼資料：

1. 執行下列任一項作業：

   * 從「資產」UI中，選取資產，然後從工具列按一下／點選「檢視屬性&#x200B;**[!UICONTROL 」圖示。]**
   * 從資產縮圖中，選擇&#x200B;**[!UICONTROL 檢視屬性]**&#x200B;快速動作。
   * 在資產頁面中，從工具列按一下／點選「檢視屬性」。****

   資產頁面會顯示資產的所有中繼資料。 此中繼資料在上傳（收錄）至AEM Assets時會自動擷取。

1. 視需要對各種標籤下的中繼資料進行編輯，在完成時，按一下工具列中的「儲存 **** 」以儲存您所做的變更。按一下/點 **[!UICONTROL 選「關閉]** 」，返回「資產」網頁介面。

   >[!NOTE]
   >
   >如果文字欄位空白，則沒有現有的中繼資料集。 您可以在欄位中輸入值，並儲存它以新增該中繼資料屬性。

對資產中繼資料所做的任何變更都會寫入原始二進位檔，作為其XMP資料的一部分。 這是透過AEM中繼資料回寫工作流程來完成的。 對現有屬性（如`dc:title`）所做的變更會被覆寫，新建立的屬性（包括如`cq:tags`的自訂屬性）會與架構一起新增。

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## 編輯元資料結構{#editing-metadata-schema}

有關如何編輯元資料架構的詳細資訊，請參閱[編輯元資料架構表單](metadata-schemas.md#edit-metadata-schema-forms)。

## 在AEM {#registering-a-custom-namespace-within-aem}中註冊自訂命名空間

您可以在AEM中新增自己的名稱空間。 就像有預先定義的名稱空間（例如cq、jcr和sling）一樣，您也可以擁有儲存庫中繼資料和xml處理的名稱空間。

1. 轉至節點類型管理頁&#x200B;*https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*。
1. 按一下或點選頁面頂端的「名稱空間&#x200B;****」。 命名空間管理頁面會顯示在視窗中。

1. 若要新增命名空間，請按一下或點選底部的&#x200B;**[!UICONTROL New]**。
1. 在XML命名空間約定中指定自訂命名空間（以URI的形式指定ID及ID的相關首碼），然後按一下或點選「儲存&#x200B;****」。
