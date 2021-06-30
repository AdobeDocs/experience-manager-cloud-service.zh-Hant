---
product: adobe experience manager
description: Adobe Experience Manager作為Cloud Service檔案。
git-repo: https://git.corp.adobe.com/AdobeDocs/experience-manager-cloud-service.zh-Hant
index: y
type: Documentation
solution: Experience Manager, Experience Manager as a Cloud Service
version: Cloud Service
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
source-git-commit: c19c15c4e71c8ead1c3cb05add052a8ffae79d0a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 6%

---


# 內部使用的中繼資料

GitHub製作系統中的中繼資料是階層式的，其定義為下列不斷提升的先例層級。

1. metadata.md
1. ToC
1. 文章

中繼資料.md檔案中定義的中繼資料會套用至整個存放庫，但可以在ToC和文章層級覆寫。 任何中繼資料的覆寫都應盡可能在最低層級完成。

experience-manager-cloud-service.en repo中的中繼資料為最低必要值。

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
* `contentOwner` (僅適用於底下的核心資產內 `/help/assets`容)
