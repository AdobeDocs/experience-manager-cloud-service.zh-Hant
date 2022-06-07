---
product: adobe experience manager
description: Adobe Experience Manager as a Cloud Service檔案。
git-repo: https://github.com/AdobeDocs/experience-manager-cloud-service.zh-Hant
index: y
type: Documentation
solution: Experience Manager
version: Cloud Service
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
source-git-commit: 5bc43af20dc8893303b1d1f4dc70939631933eb7
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 68%

---


# 內部使用的中繼資料

GitHub 編寫系統中的中繼資料具有階層式架構，而且會定義以下相對於前一項的遞增層級。

1. metadata.md
1. ToC
1. 文章

metadata.md 檔案中所定義的中繼資料會套用到整個存放庫，但可以在 ToC 和文章層級被覆寫。 中繼資料的任何覆寫都應該盡量在最低層級進行。

體驗管理器 — cloud-service.en repo中的元資料是最低要求的。

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
* `contentOwner` (僅限於 `/help/assets`)
