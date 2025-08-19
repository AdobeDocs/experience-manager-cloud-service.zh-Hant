---
title: CIF 產品輪播的自訂屬性
description: 瞭解如何更新Sling模型並自訂標籤，以擴充AEM CIF產品輪播元件。
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 758e0e13-c4d8-4d32-bcc9-91a36b3ffa98
index: false
source-git-commit: 80bd8da1531e009509e29e2433a7cbc8dfe58e60
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 3%

---


# CIF 產品輪播的自訂屬性 {#product-carousel}

瞭解如何更新Sling模型並自訂標籤，以擴充AEM CIF產品輪播元件。

## 簡介 {#intro}

產品輪播元件已在本教學課程中擴充。 首先，將產品輪播的執行個體新增至首頁，以瞭解基準線功能：

1. 導覽至網站首頁，例如[http://localhost:4502/editor.html/content/acme/us/en.html](http://localhost:4502/editor.html/content/acme/us/en.html)
1. 將新的產品輪播元件插入頁面上的主要版面容器中。

   ![產品輪播元件](/help/commerce-cloud/cif-storefront/assets/product-carousel-component.png)

1. 展開「側面板」（如果尚未切換），並將資產尋找器下拉式清單切換為&#x200B;**產品**。

   ![輪播產品](/help/commerce-cloud/cif-storefront/assets/carousel-products.png)

1. 這應該會顯示已連線之Adobe Commerce執行個體的可用產品清單。

   ![連線的執行個體](/help/commerce-cloud/cif-storefront/assets/connected-instance.png)

1. 產品將會顯示如下，並包含預設屬性：

   ![顯示具有屬性的產品](/help/commerce-cloud/cif-storefront/assets/discount.png)

## 更新Sling模型 {#update-sling-model}

您可以實作Sling模型來擴充產品輪播的業務邏輯：

1. 在您的IDE中，在核心模組下方導覽至`core/src/main/java/com/venia/core/models/commerce`，並建立可擴充CIF ProductCarousel介面的CustomCarousel介面：

   ```text
   package com.venia.core.models.commerce;
   import com.adobe.cq.commerce.core.components.models.productcarousel.ProductCarousel;
   public interface CustomCarousel extends ProductCarousel {
   }
   ```

1. 接下來，在`CustomCarouselImpl.java`建立實作類別`core/src/main/java/com/venia/core/models/commerce/CustomCarouselImpl.java`。

   Sling模型的委派模式允許`CustomCarouselImpl`透過`ProductCarousel`屬性參考`sling:resourceSuperType`模型：

   ```text
   @Self
   @Via(type = ResourceSuperType.class)
   private ProductCarousel productCarousel;
   ```

1. `@PostConstruct`註解可確保在Sling模型初始化時呼叫此方法。 產品GraphQL查詢已使用extendProductQueryWith方法擴充以擷取屬性。 更新GraphQL查詢以在部分查詢中包含屬性：

   ```javascript
   @PostConstruct
   private void initModel() {
   productsRetriever = productCarousel.getProductsRetriever();
   
   if(productCarousel.getProductsRetriever() != null)
   productCarousel.getProductsRetriever().extendProductQueryWith(p -> p
   .createdAt()
   .addCustomSimpleField("accessory_gemstone_addon")
   );
   }
   ```

   在上述程式碼中，`addCustomSimpleField`是用來擷取`accessory_gemstone_addon`屬性。

## 自訂標籤 {#customize-markup}

若要進一步自訂標示：

1. 從`productcard.html` （核心元件crxde路徑）建立`/apps/core/cif/components/commerce/productcarousel/v1/productcarousel`的復本至ui.apps模組`ui.apps/src/main/content/jcr_root/apps/venia/components/commerce/productcarousel/productcard.html`。

1. 編輯`productcard.html`以呼叫實作類別中提到的自訂屬性：

   ```xml
   ..
   <div
       data-product-sku="${product.commerceIdentifier.value}"
       data-product-base-sku="${product.combinedSku.baseSku}"
       id="${product.id}"
       data-cmp-data-layer="${product.data.json}"
       class="card product__card">
       <span>${product.product.responseData['accessory_gemstone_addon']}</span>
       <a href="${product.URL}"
           target="${productCarousel.linkTarget}"
   ..
   ```

1. 從命令列終端機，使用Maven命令儲存變更並將更新部署到AEM。 您將會在頁面上看到所選產品的自訂屬性`accessory_gemstone_addon`值。
