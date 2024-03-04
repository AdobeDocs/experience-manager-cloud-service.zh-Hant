---
product: adobe experience manager
description: Adobe Experience Manager as a Cloud Service檔案。
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.zh-Hant
index: y
type: Documentation
solution: Experience Manager, Experience Manager as a Cloud Service
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: 2b2469382fa8adfbf8a0625a90f92e27cdf53d63
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 51%

---


# 內部使用的中繼資料

GitHub編寫系統中的中繼資料具有階層式架構，而且會定義以下相對於前一項的遞增層級。

1. metadata.md
1. ToC
1. 文章

metadata.md 檔案中所定義的中繼資料會套用到整個存放庫，但可以在 ToC 和文章層級被覆寫。 中繼資料的任何覆寫都應該盡量在最低層級進行。

experience-manager-cloud-service.en存放庫中的中繼資料是最低要求。

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

ToCs

* `sub-product`
* `user-guide-title`

文章

* `title`
* `description`
* `contentOwner` （僅針對下的核心資產內容） `/help/assets`)
