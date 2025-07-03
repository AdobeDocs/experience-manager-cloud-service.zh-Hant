---
title: CIF產品和類別選擇器的使用方式
description: 瞭解如何在您的客戶商務元件中使用CIF產品和類別選擇器，以支援作者和行銷人員有效使用商務產品和目錄資料。
sub-product: Commerce
topics: Development
version: Experience Manager as a Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 30f1f263-1b78-46ae-99ed-61861c488b2a
role: Admin
index: false
source-git-commit: 173b70aa6f9ad848d0f80923407bf07540987071
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# AEM內容與Commerce編寫選擇器 {#cif-pickers}

AEM內容與Commerce製作提供一套製作工具，可協助AEM作者和行銷人員有效使用商務產品資料和目錄。 產品選擇器和類別選擇器屬於CIF附加元件的一部分，並由CIF核心元件使用。 專案可以在任何元件對話方塊中使用這些選擇器來選取產品或類別。

## 產品挑選器 {#product-picker}

若要在專案元件中使用產品選擇器，開發人員必須將`commerce/gui/components/common/cifproductfield`新增至元件對話方塊。 例如，對`cq:dialog`使用以下專案：

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

產品欄位可讓您透過不同檢視，導覽至使用者想要選取的產品。 依預設，產品欄位會傳回產品的ID，但可使用`selectionId`屬性進行設定。

產品選取器欄位支援下列選擇性屬性：

- selectionId (id、uid、SKU、slug、combinedSlug、combinedSku) — 可讓您選擇選擇器要傳回的產品屬性（預設值= id）。 使用SKU會傳回所選產品的SKU。 使用combinedSku會傳回base#variant之類的字串以及基礎產品和所選取變體的SKU，或是傳回單一SKU （如果已選取基礎產品）。
- filter (folderOrProduct， folderOrProductOrVariant) — 篩選在導覽產品樹狀結構時挑選器要呈現的內容。 folderOrProduct — 轉譯資料夾和產品。 folderOrProductOrVariant — 轉譯資料夾、產品和產品變體。 如果轉譯了產品或產品變體，也可在選擇器中選取它。 （預設= folderOrProduct）
- 多個(true， false) — 啟用選取一或多個產品的功能（預設= false）
- emptyText — 設定選擇器欄位的空白文字值

也支援標準對話方塊欄位屬性，例如`name`、`fieldLabel`或`fieldDescription`。

>[!CAUTION]
>
>`cifproductfield`元件需要`cif.shell.picker` clientlib。 若要將clientlib新增至對話方塊，您可以使用extraClientlibs屬性。
>&#x200B;>[!CAUTION]
>
>從CIF核心元件2.0.0版開始，已移除對`id`的支援，並取代為`uid`。 Adobe建議使用`sku`或`slug`作為產品識別碼。 Adobe僅繼續為使用CIF核心元件1.x版的專案支援`id`。

在`cifproductfield`CIF核心元件[專案中可以找到](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml)的完整工作範例。 另請參閱AEM核心元件檔案的[自訂對話方塊](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=zh-Hant#customizing-dialogs)。

## 類別選取器 {#category-picker}

類別選擇器可用於元件對話方塊中，其使用方式與產品選擇器類似。

以下程式碼片段可用於cq：dialog設定：

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

類別選擇器欄位支援下列選擇性屬性：

- selectionId(id， uid， slug， urlPath， idAndUrlPath _（已棄用）_， uidAndUrlPath _（已棄用）_) — 可讓您選擇選擇器要傳回的類別屬性（預設值= id）。
- multiple (true， false) — 啟用選取一或多個類別（預設= false）

也支援標準對話方塊欄位屬性，例如`name`、`fieldLabel`或`fieldDescription`。

>[!CAUTION]
>
>與`cifproductfield`元件相同，`cifcategoryfield`元件也需要`cif.shell.picker` clientlib。 若要將clientlib新增至對話方塊，您可以使用`extraClientlibs`屬性。 請參閱AEM核心元件檔案的[自訂對話方塊](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=zh-Hant#customizing-dialogs)。
>&#x200B;>[!CAUTION]
>
>從CIF核心元件2.0.0版開始，已移除對`id`的支援，並取代為`uid`。 Adobe建議使用`uid`或`urlPath`作為類別識別碼。 Adobe繼續僅對使用CIF核心元件1.x版的專案支援`id`和`idAndUrlPath`。

在`cifcategoryfield`CIF核心元件[專案中可以找到](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml)的完整工作範例。
