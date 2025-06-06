---
title: JSON-LD中繼資料
description: 瞭解如何在AEM CIF中啟用及驗證JSON+LD功能。
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 547d3721-e094-4a42-8a7c-27e4ef97ea9c
source-git-commit: 6ee09ab274e26f6972a81e662b78030a71b3fc9b
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 2%

---

# JSON-LD中繼資料 {#json-ld}

本指南說明如何在AEM CIF中啟用及驗證JSON+LD功能。

>[!NOTE]
>
> 此功能屬於實驗性質。

## 在CIF設定中啟用JSON+LD {#enabling}

依預設，**啟用JSON+LD**核取方塊在CIF設定中不可見。 若要啟用此功能，專案必須包含必要的OSGi設定，以便顯示核取方塊。 此設定可讓使用者切換產品頁面上的JSON+LD指令碼支援。
若要讓**啟用JSON+LD**&#x200B;核取方塊可在CIF設定中使用，請將下列OSGi設定新增至您的專案： `
com.adobe.cq.cif.components.models.JsonLdFeatureEnable`。
如需新增此設定的詳細資訊，請參閱公用aem-cif-guides-venia存放庫中的[新增Json-Ld](https://github.com/adobe/aem-cif-guides-venia/blob/main/ui.config/src/main/content/jcr_root/apps/venia/osgiconfig/config/com.adobe.cq.cif.components.models.JsonLdFeatureEnable.cfg.json)的設定。

新增及部署此設定後，CIF設定中就會顯示核取方塊，以下是啟用&#x200B;**JSON+LD**&#x200B;的步驟：

1. 導覽至AEM中的CIF設定。
1. 取消繼承。
1. 勾選&#x200B;**啟用JSON+LD**&#x200B;核取方塊。
1. 儲存設定。

## 在產品詳細資料頁面(PDP)上驗證JSON+LD {#verify}

為了說明驗證JSON+LD的步驟，以Venia專案為例，其中已新增必要的JSON+LD設定來啟用該功能。 以下是需遵循的步驟：

1. 導覽至您的本機AEM執行個體，然後開啟產品詳細資料頁面(PDP)： http://localhost:4502/editor.html/content/venia/us/en/products/product-page.html
1. 在產品詳細資料頁面(PDP)上製作產品。
1. 切換至&#x200B;**以發佈**&#x200B;模式檢視。
1. 在瀏覽器中開啟&#x200B;**檢視頁面Source**。
1. 在頁面來源中搜尋JSON+LD。

如果設定正確，您會發現與插入頁面中的產品相關聯的JSON+LD指令碼。

## 產品的JSON+LD結構範例 {#sample}

以下是在Venia專案的PDP頁面上編寫的Agatha Shirt的範例&#x200B;**JSON+LD**&#x200B;結構：

```
<script type="application/ld+json">
{
  "@context": "http://schema.org",
  "@type": "Product",
  "sku": "VSK05",
  "name": "Agatha Skirt",
  "image": "https://mcstaging.catalogservice4commerce.fun/media/catalog/product/cache/926ea6fc2ad48a7202ff4587b6c2768e/v/s/vsk05-pe_main_2.jpg",
  "description": "The Agatha Skirt has a large circumference that lends itself to all sorts of drama...",
  "@id": "product-ef4fa1dc72",
  "offers": [
    {
      "@type": "Offer",
      "sku": "VSK05-KH-S",
      "url": "/content/venia/us/en/products/product-page.html/agatha-skirt.html",
      "priceCurrency": "USD",
      "price": 78.0
    },
    {
      "@type": "Offer",
      "sku": "VSK05-RN-XS",
      "availability": "InStock",
      "priceSpecification": {
        "@type": "UnitPriceSpecification",
        "priceType": "https://schema.org/ListPrice",
        "price": 18.0,
        "priceCurrency": "USD"
      },
      "price": 46.0
    }
  ]
}
</script>
```

## 將JSON+LD屬性對應至GraphQL {#mapping}

JSON+LD屬性可對應至AEM CIF中的GraphQL查詢，確保結構化資料會動態反映透過GraphQL擷取的產品資訊。

### 產品對應範例 {#example}

| JSON+LD屬性 | Magento GraphQL屬性 | 必填(Y/N) |
|---------------------------------|-------------------|---|
| sku | sku | N |
| offers.url | 自訂邏輯 | N |
| offers.SpecialPricedate | special_to_date | N |
| offers.sku | sku | N |
| offers.priceSpecification.priceCurrency | 貨幣 | Y |
| offers.priceSpecification.price | regular_price | N |
| offers.priceCurrency | 貨幣 | Y |
| offers.price | special_price | Y |
| offers.image | media_gallery.url | N |
| offers.availability | stock_status | N |
| 名稱 | 名稱 | Y |
| 影像 | media_gallery.url | Y |
| 說明 | 說明 | N |
| aggregateRating.reviewCount | review_count | N |
| aggregateRating.ratingValue | rating_summary | N |
| @id | id | N |

此對應程式可確保根據透過GraphQL查詢擷取的產品資料，動態填入JSON+LD指令碼。

若要測試您的JSON+LD結構，您可以使用[Rich Results測試 — Google搜尋主控台](https://search.google.com/test/rich-results/result?id=wtU3LVIEM8H7Aaf5qqK9qw)。 此工具提供詳細的意見回饋，包括所需屬性是否存在或遺失，並協助確保結構化資料正確實作。
