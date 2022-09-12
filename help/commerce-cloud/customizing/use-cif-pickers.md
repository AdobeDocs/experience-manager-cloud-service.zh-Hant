---
title: CIF產品和類別選擇器的使用
description: 了解如何在客戶商務元件中使用CIF產品和類別選擇器，以支援作者和行銷人員有效處理商務產品和目錄資料。
sub-product: Commerce
topics: Development
version: Cloud Service
activity: develop
audience: developer
feature: Commerce Integration Framework
exl-id: 30f1f263-1b78-46ae-99ed-61861c488b2a
source-git-commit: f5e465d90477f1b49e4ff1c5ca9dd47cc5d539bb
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# AEM內容與商務製作選擇器 {#cif-pickers}

AEM內容與商務製作提供一組製作工具，可協助AEM作者和行銷人員有效處理商務產品資料和目錄。 產品選擇器和類別選擇器是CIF附加元件的一部分，並供CIF核心元件使用。 專案可在任何元件對話方塊中使用這些選取器來選取產品或類別。

## 產品挑選器 {#product-picker}

若要在專案元件中使用產品選擇器，開發人員必須新增 `commerce/gui/components/common/cifproductfield` 至元件對話方塊。 例如，對cq使用下列項目:dialog:

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

產品欄位可導覽至使用者要透過不同檢視選取的產品。 依預設，產品欄位會傳回產品的ID，但可使用 `selectionId` 屬性。

產品選擇器欄位支援下列可選屬性：

- selectionId(id、uid、sku、snug、combinedSlug、combinedSku) — 可選取器要傳回的產品屬性（預設= id）。 使用sku會傳回所選產品的SKU，而使用combinedSku並傳回字串，例如base#variant與基本產品和所選變體的SKU，或如果選取了基本產品，則傳回單一SKU。
- filter(folderOrProduct、folderOrProductOrVariant) — 篩選器在導覽產品樹狀結構時要由選擇器呈現的內容。 folderOrProduct — 轉譯資料夾和產品。 folderOrProductOrVariant — 轉譯資料夾、產品和產品變體。 如果轉譯了產品或產品變體，也可在選擇器中選取它。 （預設= folderOrProduct）
- 多個(true, false) — 啟用選取一或多個產品（預設= false）
- emptyText — 配置選擇器欄位的空文本值

此外，標準診斷欄位屬性，如 `name`, `fieldLabel`，或 `fieldDescription` 也受支援。

>[!CAUTION]
>
>此 `cifproductfield` 元件需要 `cif.shell.picker` clientlib 。 若要將clientlib新增至對話方塊，您可以使用extraClientlibs屬性。
>[!CAUTION]
>
>從CIF核心元件2.0.0版開始，即可支援 `id` 已移除並取代為 `uid`. 強烈建議使用 `sku` 或 `slug` 作為產品識別碼。 我們繼續支援 `id` 僅適用於使用CIF核心元件1.x版的專案。

的完整運作範例 `cifproductfield` 可在 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml) 專案。 另請參閱 [自訂對話方塊](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) 的AEM核心元件說明檔案。

## 類別選擇器 {#category-picker}

類別選擇器也可以像產品選擇器一樣，在元件對話方塊中使用。

下列程式碼片段可用於cq:dialog設定：

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

類別選擇器欄位支援下列可選屬性：

- selectionId(id, uid, srug, urlPath, idAndUrlPath _（已過時）_, uidAndUrlPath _（已過時）_) — 可選擇選擇器要傳回的類別屬性（預設= id）。
- 多個(true, false) — 啟用選取一或多個類別（預設= false）

此外，標準診斷欄位屬性，如 `name`, `fieldLabel`，或 `fieldDescription` 也受支援。

>[!CAUTION]
>
>與 `cifproductfield` 元件 `cifcategoryfield` 元件也需要 `cif.shell.picker` clientlib 。 若要將clientlib新增至對話方塊，您可以使用 `extraClientlibs` 屬性。 請參閱 [自訂對話方塊](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) 的AEM核心元件說明檔案。
>[!CAUTION]
>
>從CIF核心元件2.0.0版開始，即可支援 `id` 已移除並取代為 `uid`. 強烈建議使用 `uid` 或 `urlPath` 作為類別識別碼。 我們繼續支援 `id` &amp; `idAndUrlPath` 僅適用於使用CIF核心元件1.x版的專案。

的完整運作範例 `cifcategoryfield` 可在 [CIF核心元件](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml) 專案。
