---
title: 如何編輯或添加元資料
description: 瞭解中的資產元資料 [!DNL Experience Manager Assets] 可通過多種方式編輯資產元資料。
contentOwner: AG
feature: Metadata
role: User,Admin
exl-id: 464a97ce-da3e-47b5-9879-fafaf2f2378c
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 7%

---

# 如何編輯或添加元資料 {#how-to-edit-or-add-metadata}

元資料是可搜索的資產的其他資訊。 上載影像時，系統會自動提取影像。 您可以編輯現有元資料或向現有欄位添加新元資料屬性（例如，當元資料欄位為空時）。

因為公司需要可控且可靠的元資料辭彙， [!DNL Experience Manager Assets] 不允許臨時添加新元資料屬性。 雖然作者無法為資產添加新的元資料欄位，但開發人員可以。 請參閱 [為資產建立新元資料屬性](meta-edit.md#editing-metadata-schema)。

## 編輯資產的元資料 {#editing-metadata-for-an-asset}

要編輯元資料：

1. 執行下列操作之一：

   * 在「資產」UI中，選擇資產，然後按一下/點擊 **[!UICONTROL 查看屬性]** 的子菜單。
   * 從資產縮略圖中，選擇 **[!UICONTROL 查看屬性]** 快速操作。
   * 在資產頁面中，按一下/點擊 **[!UICONTROL 查看屬性]** 的子菜單。

   資產頁面顯示資產的所有元資料。 元資料在上傳（攝入）到Experience Manager Assets時被自動提取。

1. 視需要對各種標籤下的中繼資料進行編輯，在完成時，按一下工具列中的「儲存 **** 」以儲存您所做的變更。按一下/點 **[!UICONTROL 選「關閉]** 」，返回「資產」網頁介面。

   >[!NOTE]
   >
   >如果文本欄位為空，則不存在現有元資料集。 您可以在欄位中輸入一個值並保存該值以添加該元資料屬性。

對資產元資料的任何更改都作為其資料的一部分寫回原始二進位XMP檔案。 這是通過Experience Manager元資料回寫工作流完成的。 對現有物業(如 `dc:title`)被覆蓋並新建屬性(包括自定義屬性，如 `cq:tags`)與架構一起添加。

<!-- XMP write-back is supported and enabled for the platforms and file formats described in technical requirements. -->

## 編輯元資料架構 {#editing-metadata-schema}

有關如何編輯元資料架構的詳細資訊，請參見 [編輯元資料架構表單](metadata-schemas.md#edit-metadata-schema-forms)。

## 在Experience Manager中註冊自定義命名空間 {#registering-a-custom-namespace-within-aem}

可以在Experience Manager中添加您自己的命名空間。 正如存在預定義的命名空間（如cq、jcr和sling）一樣，您也可以為儲存庫元資料和xml處理提供一個命名空間。

1. 轉到節點類型管理頁 *https://&lt;host>:&lt;port>/crx/explorer/nodetypes/index.jsp*。
1. 按一下或點擊 **[!UICONTROL 命名空間]** 頁面頂部。 命名空間管理頁顯示在窗口中。

1. 要添加命名空間，請按一下或點擊 **[!UICONTROL 新建]** 在底部。
1. 在XML命名空間約定中指定自定義命名空間（以URI和ID的關聯前置詞的形式指定ID），然後按一下或點擊 **[!UICONTROL 保存]**。
